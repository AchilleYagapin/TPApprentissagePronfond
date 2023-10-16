
Please, download the data from https://drive.google.com/drive/folders/1HOswvH42by9wsS26SbCqfRMfNeqGh6Xa?usp=share_link


import os
import PIL
class SiameseNetworkDataset():
    def __init__(self,train_file=None,base_dir=None,transform=None):
        print(base_dir,train_file)
        self.train_pairs=np.load(train_file)
        self.base_dir = base_dir
        self.transform = transform

    def __getitem__(self,index):
        img0 = PIL.Image.open(self.base_dir+self.train_pairs[index,0]).convert("L")
        img1 = PIL.Image.open(self.base_dir+self.train_pairs[index,1]).convert("L")
        if self.transform is not None:
            img0 = self.transform(img0)
            img1 = self.transform(img1)
        return img0, img1 , torch.from_numpy(np.array([int(self.train_pairs[index,2])],dtype=np.float32))

    def __len__(self):
        return len(self.train_pairs)

#train_set = SiameseNetworkDataset(base_dir+'train_pairs.npy',base_dir=base_dir+'train/',transform=torchvision.transforms.Compose([torchvision.transforms.Resize((105,105)),torchvision.transforms.ToTensor()]))
#test_set  = SiameseNetworkDataset(base_dir+'test_pairs.npy',base_dir=base_dir+'test/',transform=torchvision.transforms.Compose([torchvision.transforms.Resize((105,105)),torchvision.transforms.ToTensor()]))
train_set = SiameseNetworkDataset(base_dir+'train_pairs.npy',base_dir=base_dir+'train/',transform=torchvision.transforms.Compose([torchvision.transforms.Resize((20,20)),torchvision.transforms.ToTensor()]))
test_set  = SiameseNetworkDataset(base_dir+'test_pairs.npy',base_dir=base_dir+'test/',transform=torchvision.transforms.Compose([torchvision.transforms.Resize((20,20)),torchvision.transforms.ToTensor()]))
batch = next(iter(torch.utils.data.DataLoader(train_set,shuffle=True, batch_size=15)))
image_set = torch.cat((batch[0],batch[1]),0)
plt.imshow(np.transpose(torchvision.utils.make_grid(image_set), (1, 2, 0)))
print('labels',batch[2].numpy().ravel())
