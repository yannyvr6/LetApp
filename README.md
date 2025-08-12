# LetApp
This is a Recipe App for personal use.

It also comes with a grocery List for each receipe and a weeekly meal plan.

App is still in the works but will keep updating it! 🧚‍♂️✨

The Original instructions for this the launching of the app come from https://github.com/Btelgeuse/DesktopAppTutorial

She is an amazing content creator and porgrammer. 

Here are the steps taken:

1. Create a new repository on GitHub
2. Open VSCode
3. Create a folder for your application
4. In the same folder, create index.html and index.js files
5. In this folder, write "npm init" command (verify that you are in the correct folder in the terminal!)
6. Then write "npm install --save-dev electron" command (verify that you are in the correct folder in the terminal!)
7. A file package.json should have been added. add the following command in the scripts part:  "start": "electron ."

8. For the window setup, write these commands in your index.js:

const path = require("path");
const { app, BrowserWindow, ipcMain } = require("electron");
const fs = require("fs");

let win;

function createWindow() {
  win = new BrowserWindow({
    width: 550,
    height: 600,
    webPreferences: {
      nodeIntegration: false,
      contextIsolation: true,
      preload: path.join(__dirname, "preload.js"),
    },
  });

  win.removeMenu();
  win.loadFile("index.html");
  
  ipcMain.on("load-page", (event, page) => {
    win.loadFile(page);
  });
}

app.whenReady().then(() => {
  createWindow();
  app.on("activate", () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow();
    }
  });
});

9. Still for the window setup, write these commands in a new file preload.js:

const { contextBridge, ipcRenderer } = require("electron");

contextBridge.exposeInMainWorld("electronAPI", {
  loadPage: (page) => ipcRenderer.send("load-page", page),
});

10. Init GitHub in your app folder using "git init" (verify that you are in the correct folder in the terminal!)
11. Connect this folder to your GitHub repository using the "git remote add origin ..." command with your repository URL.
12. Now to avoid pushing a too heavy file to GitHub, we will have to create a new file .gitignore that contains at least this line: node_modules/
(You can see my .gitignore file that contains more elements for git to ignore)
13. To make your folder even less heavy, write "git lfs install" command (verify that you are in the correct folder in the terminal!) and write these commands:

git lfs track "*.png"
git lfs track "*.jpg"
git lfs track "*.psd"
git lfs track "*.mp4"
git lfs track "*.exe"

14. Now you can push your app project on Github using the commands:

git add .
git commit -m 'initialization'
git push -u origin master

15. To run your application, write "npm start" in your terminal (verify that you are in the correct folder in the terminal!)
16. To make your application a ready-to-use desktop application, write these commands in your terminal:

npm install --save-dev @electron-forge/cli
npm exec --package=@electron-forge/cli -c "electron-forge import"
npm run make


For the personal part of the code the following steps were taken:

1. 