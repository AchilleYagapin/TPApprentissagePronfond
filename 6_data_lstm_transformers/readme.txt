Les deux fichiers de données pour le TP du bloc 5.


# modèle

class mymodel(torch.nn.Module):
    def __init__(self):
        super().__init__()
        self.eb = torch.nn.Embedding(num_codes, embedding_size)
        self.hidden_size = 256
        self.num_layers = 2
        self.rnn = torch.nn.LSTM(input_size = embedding_size, hidden_size = self.hidden_size, num_layers = self.num_layers, batch_first=True)
        self.l = torch.nn.Linear(self.hidden_size,num_codes)


     
    def forward(self, x_src):
      output, (hn, cn) = self.rnn(self.eb(x_src))
      res = self.l(output.reshape(-1,output.shape[2]))
      res = res.reshape(x_src.shape[0],x_src.shape[1],-1)
      return res 



#entrainement

import pathlib

embedding_size=20
learning_rate = 1e-3
model = mymodel()
model.training = True
optimizer = torch.optim.Adam(model.parameters(), lr=learning_rate)   

NUM_EPOCH=50
 
for epoch in range(NUM_EPOCH):
  global_loss=0
  for x_src, x_tgt in train_loader:
    optimizer.zero_grad()
    x_tgt_pred = model(x_src)
    x_tgt_output = torch.clone(x_tgt[:,:]).reshape(x_src.shape[0]*x_src.shape[1])
    loss = torch.nn.CrossEntropyLoss()(x_tgt_pred.reshape(x_src.shape[0]*x_src.shape[1],-1),x_tgt_output)
    loss.backward()
    optimizer.step()
    global_loss = global_loss+loss.detach().cpu().numpy()
  if epoch%10==0:
      print('epoch: ',epoch, 'loss: ',global_loss)
      print("exemple de décodage d'une donnée de train : ",ascii2str(x_tgt[0,:]),' -> ',ascii2str(torch.argmax(x_tgt_pred,axis=2)[0]),'<fin>')
      my_file = pathlib.Path('./model_transformer2.pt')
      torch.save({'optimizer':optimizer.state_dict(), 'model':model.state_dict()}, my_file)


# décodage test
model.training = False
for x_src, x_tgt in test_loader:
  y_pred = model(x_src)
  y_pred = torch.argmax(y_pred,axis=2)
  for i in range(x_src.shape[0]):
    print("décodage de [", ascii2str(x_src[i]),"] -> [",ascii2str(y_pred[i]) ,"] GT = ",ascii2str(x_tgt[i]))
    break
