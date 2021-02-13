# Builds

# dogecoin-bootstrap

## 2020-01-29: Latest torrent file for a up to date chain (uncompressed) available at https://dogecoin.gg/dogecoin-bootstrap-2021-01-29.torrent (Hosted/Maintained by https://github.com/IncognitoJam/IncognitoJam )

Yoinked instructions:
```
You can use the bootstrap to get started more quickly with Dogecoin Core, you don't have to wait as long to synchronise the entire chain.

Make sure you are using the latest Dogecoin Core 1.14.2! Run the wallet once and then close it.

Download: https://dogecoin.gg/dogecoin-bootstrap-2021-01-29.torrent
Torrent Hash: 9aaaa5c4bd18686d49d6fce7758409349c62567b

After downloading the .torrent, open it with your torrent client of choice, and download it. It's around 45GB.

Once  finished, navigate to your dogecoin data directory:
Windows: C:\Users\USER\AppData\Local\Dogecoin
Linux: ~/.dogecoin/
macOS: ~/Library/Application Support/Dogecoin/
(Can't find it? You can check the path by going to Help -> Debug window -> Information -> Datadir)

Make sure your Dogecoin Core client is not running, then clear out the contents of the blocks and chainstate folders (NOTE: make sure you are NOT deleting any wallet.dat files or you will lose your coins!) and copy in the files from the bootstrap you just downloaded. 

After you drop those files into the appropriate folders start up Dogecoin Core. Wait for indexing to finish, and then it will start synchronising from 29th January 2021.
```
