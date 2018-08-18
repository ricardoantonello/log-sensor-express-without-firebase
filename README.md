# log-sensor-express (in progress)
Logs sensor data (DHT11) in local data base (sqlite), visualize in browser (express and chart.js) and backup online in firebase.  
Main reference (e-Book): Full Stack Web Development with Raspberry Pi 3 (Packt).  
My site: https://cv.antonello.com.br  

# Node and Express install instructions
### First, install the curl command:
sudo apt-get update && sudo apt-get install curl
### Then, install nvm via the install script:
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
nvm --version  
nvm install 6  
### Will look like this:
pi@raspberrypi:~ $ node -v  
v6.10.2  
pi@raspberrypi:~ $ npm -v  
3.10.10  
### Create git
mkdir sensor-project  
mkdir sensor-project/hello-world  
touch sensor-project/hello-world/hello-world.js  
cd sensor-project  
git init  
### Add all files to staging area
git add -A  
### Commit to repository. Mark the commit with a message
git commit -m "Initialized first project"  
### Add the remote link
git remote add origin https://my-remote-repo-url.com/sensor-project.git  
### Push all changes to the remote repo  
git push origin master  

### On Raspberry Pi 3
Now, all your code is present on the cloud. All you have to do now is go into your Raspberry Pi's Terminal and run this:  
git clone https://my-remote-repo-url.com/sensor-project.git  
cd ~/sensor-project  
#### You now have the project fully cloned on your Pi. To make changes and reflect them on your Pi, first, make the changes to files or folders on your computer and then add and push the changes to the repository:  
git add -A  
git commit -m "Made some changes"  
git push origin master  

#### Then on your Pi, run this:
cd ~/sensor-project  
git pull origin master  

## Create your express project
mkdir server  
cd server  
npm init // script that creates package.json, etc...  
echo "node_modules" >> .gitignore  

#### After that and with index.js completed you can run the server (server is the folder where you have the index.js)
node server  

# APENDICE Github (in brazilian portuguese ;)
### Minha sugestao é criar o repositorio online, fazer o clone para baixar para a maquina local, incluir e alterar os arquivos e depois add, commit e push...
git clone  <git adress>  
git add -A  
git commit -m "mensagem para commit"  
git push

#### Para baixar atualizações da nuvem em repo já foi criado (via init ou clone)
git pull  

### Para criar do zero um repo localmente
#### Change the current working directory to your local project.
git init #Initialize the local directory as a Git repository.  
git add . # Adds the files in the local repository and stages (organize) them for commit. To unstage a file, use 'git reset HEAD YOUR-FILE'.  
git commit -m "First commit" # Commits the tracked changes and prepares them to be pushed to a remote repository. To remove this commit and modify the file, use 'git reset --soft HEAD~1' and commit and add the file again.  
git remote add origin remote repository URL # Sets the new remote  
git remote -v ## Verifies the new remote URL  
git push origin master # Pushes the changes in your local repository up to the remote repository you specified as the origin  
#### Importing a Git repository using the command line (from another user) 
git clone https://external-host.com/extuser/repo.git # cria a pasta repo.git  
cd repo.git  
git push --mirror https://github.com/ghuser/repo.git # Pushes the mirror to the new GitHub repository  
cd .. E rm -rf repo.git # apaga a pasta temporaria  

## Keeping the server running in the background
npm install -g pm2  
The -g flag indicates that we want to install the pm2 module globally and not just in our project directory. What this will also do is install any binaries the module has as command-line tools.
pm2 --version  
pm2 start server/  

## pm2 on python
If you're working with Python, remember that pm2 can run scripts .py to.  
Example: pm2 start "python3 run.py runserver" --name flaskserver  

## Reading DHT11 sensor
git clone git://git.drogon.net/wiringPi  
cd wiringPi/  
./build  
gpio -v
wget http://www.airspayce.com/mikem/bcm2835/bcm2835-1.52.tar.gz  
tar -xvzf bcm2835-1.52.tar.gz  
cd bcm2835-1.52  
./configure  
make  
sudo make check  
sudo make install
npm install --save node-dht-sensor

## Instaling Chart.js
npm install chart.js --save

## Instaling Sqlite3
npm install sqlite3

sudo apt-get update  
sudo apt-get install sqlite3  
sqlite3 --version  
sqlite # entra no prompt de comando do sqlite3
#### Comands examples
CREATETABLE temperature (createdAt TEXT,valueREAL);  
CREATETABLE humidity (createdAt TEXT,valueREAL);  
.tables # to list tables  
INSERT INTO temperature VALUES(datetime('now'),16.7);  
SELECT * FROM temperature;  
SELECT"value"from temperature;  
SELECT*FROM temperature WHERE createdAt >"2017-06-18"  
SELECT"value"FROM temperature WHERE createdAt >"2017-06-18 12:26:09";  
UPDATE <table name> SET <colum name>=<new value> WHERE <filter condition>;  
UPDATE temperature SET value=16.6 WHERE createdAt="2017-06-18 12:26:08";  
DELETE FROM <table name> WHERE <filter condition>;  
SELECT avg(value) FROM temperature;  
SELECT max(value) FROM temperature;  
SELECT max(value) FROM temperature WHERE createdAt < "2017-06-18 12:26:10";  
SELECT * FROM temperature WHERE value > (SELECT avg(value) FROM temperature);  
SELECT value, (SELECT avg(value) FROM temperature)-value as deviation, createdAt FROM temperature;

## Instaling Socket.io
npm install --save socket.io