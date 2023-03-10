# Flutter Skeleton

```
boilerplate code giving you the start of a flutter app connected to firebase.

if a user exists in auth, they will be directed to the profile screen after logging in.
if a user has not logged in before, they will be directed to a create profile screen.

app includes:

- login screen
- create profile screen
- profile screen
- nav drawer
- provider state management

this app is connected to a node.js back end that makes all firebase calls
```

## Get the Flutter App and Create Firebase Project

#### Forking the Repository

- Click the "Fork" button in the top right corner of the page.
- Select the account you want to fork the repository to.

  Once the fork is complete, you will have a copy of the repository in your account.

#### Cloning the Forked Repository to Your Local Machine

- Open a terminal window.
- Navigate to the directory where you want to clone the repository.
- Run the following command, replacing <repo-name> with the name of your fork:

        git clone https://github.com/<your-username>/<repo-name>.git

  This will create a new directory with the name of the repository, and clone the repository files into it.

#### Creating a Firebase Project

- Go to the [Firebase Console](https://console.firebase.google.com/).
- Click the "Add project" button.
- Follow the prompts to create a new project.

## Connect Firebase Project to Your Flutter App
<img width="392" alt="Screenshot 2023-01-02 at 1 01 53 PM" src="https://user-images.githubusercontent.com/35585020/210274367-183e9950-65eb-4711-ae38-a718a21bb7b5.png">

After creating the Firebase project, click the Flutter icon and follow the prompts to connect the Firebase project to your Flutter App.

<img width="477" alt="Screenshot 2023-01-02 at 1 48 07 PM" src="https://user-images.githubusercontent.com/35585020/210277000-8daccd79-cdef-4124-b107-ff212f218fe4.png">

*Note that you do not need to create a new Flutter project, as are using the cloned Flutter project repository*

<img width="723" alt="Screenshot 2023-01-02 at 1 54 38 PM" src="https://user-images.githubusercontent.com/35585020/210277399-8c843fb4-c8fb-4f0e-87dd-7781f8e8893d.png">

If you get the following warning after running `dart pub global activate flutterfire_cli`:

    Warning: Pub installs executables into $HOME/.pub-cache/bin, which is not on your path.
  
Run the following command:

    export PATH="$PATH":"$HOME/.pub-cache/bin"

After registering your per-platform apps with Firebase, in the terminal, you are prompted to select the platforms you want the Flutter project to support. Select all platforms and say yes to every prompt.

<img width="724" alt="Screenshot 2023-01-02 at 1 40 59 PM" src="https://user-images.githubusercontent.com/35585020/210276544-23a7b840-62ea-47a2-8486-ff3c1c213a1e.png">

You do not need to do this, it is already in the code.

## Enable Firebase Products

Now that you have connected your Flutter app to Firebase, you need to enable the Firebase products that the app is using.

In the Firebase console, go to `All Products`

You need to turn on and go through the prompts for each product.

#### Authentication
- Click `Get Started` button
- Select `Email/Password` as the sign-in provider

#### Storage and Firestore Database
- Click `Get Started` button
- Keep everything as is and go through the prompts
- Click `Rules` tab
- Edit the rules to:
```
rules_version = '2';
service cloud.firestore {
match /databases/{database}/documents {
 match /{document=**} {
  allow read, write: if true;
  }
 }
}
```

#### Functions
- Upgrade plan, if you have not done so already
- Follow prompts
- After running the `firebase init` command
  - Select `Emulators`
  - Use existing project
  - Select Firebase project that you just made
  - Make sure `Authentication` , `Firestore`, `Storage`, and `Functions` are selected
  - Download emulators
- You do not need to run `firebase deploy`, because you are running on an emulated environment

## Get Credentials and Run Emulator
  
#### Get Google Credentials
  - Go to Project Settings in the Firebase Console
  - Select `Service accounts` tab
  - Generate new private key
  - Save key in safe location
  
#### Run Emulator

- cd lib/back_end/functions
- Run: 

        npm install
    
- cd /lib/back_end
- Run: 

        export GOOGLE_APPLICATION_CREDENTIALS='path/to/credentials.json'
    
- Run: 

        firebase emulators:start
    
## Run Flutter App

- Open new terminal window 
- cd root of Flutter app
- Run:

        flutter run
