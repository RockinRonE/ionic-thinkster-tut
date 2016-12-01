Currently our app shows a location and a todo that is hard coded. Before we get into how to make this dynamic we should think about how we want our todo list data modeled. Since Ionic does not have a model generator we’ll have to create it ourselves. 

Lets get started by creating a new directory inside **src** called **models. **

**
**

Then create a file called **todolist-model.ts** in this directory like so:

![Screen Shot 2016-12-01 at 3.54.02 PM.png](resources/86219DBCBC00715C263CDAC24038046C.png)



### Create a Provider

We’ll need a data service to save and retrieve data from storage. This can be generated using Ionic’s CLI by running: 

`ionic g provider Data`​

This command will generate a **providers** directory that contains **data.ts**. We’ll need to import this and add it to our `providers` array in **app.module.ts:**

```js
import { NgModule } from '@angular/core';
import { IonicApp, IonicModule } from 'ionic-angular';
import { MyApp } from './app.component';

import { Storage } from '@ionic/storage';
import { Data } from '../providers/data'; 

import { HomePage } from '../pages/home/home';
import { TodolistPage } from '../pages/todolist-page/todolist-page';

@NgModule({
  declarations: [
    MyApp,
    HomePage,
    TodolistPage
  ],
  imports: [
    IonicModule.forRoot(MyApp)
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp,
    HomePage,
    TodolistPage
  ],
  providers: [Storage, Data]
})
export class AppModule {}

```

Adding a New Location Form
--------------------------

Lets start by building out our `add-circle` button at the upper right-hand corner on our Location list page. We’ll be taking advantage of Ionic’s [AlertController](http://ionicframework.com/docs/v2/api/components/alert/AlertController/) to take in the location name of our todo list. To do this we’ll first have to import it in **home.ts** by adding **AlertController** to the import line of ‘ionic-angular' :

```js
import { NavController, AlertController } from 'ionic-angular';
```

Then we need to add it to our constructor:

```js
constructor(public navCtrl: NavController, public alertCtrl: AlertController) {
    
  }
```

And now we can use it in our class as so:

```js
addLocationlist(): void {

    let prompt = this.alertCtrl.create({
      
      title: 'New Location',
      message: 'Enter the name of your new location:',
      inputs: [
        {
          name: 'location'
        }
      ],
      buttons: [
        {
          text: 'Cancel'
        },
        {
          text: 'Save',
          handler: data => {
            console.log('Data saved!');
          }
        }
      ]
    });
    
    prompt.present(); 
    
  }
```

Lets now update **home.html** to invoke our function:

```js
<ion-buttons end>
    <button ion-button icon-only (click)="addLocationlist()" >
      <ion-icon name="add-circle"></ion-icon>
    </button>
</ion-buttons>
```

Now when you click our `add-circle` button you should see

![Screen Shot 2016-12-01 at 12.22.56 PM.png](resources/A234417BE6C4EB0E5FCEABC191E32552.png)

If you hit save you’ll see our “Data saved!” in the console.

Capturing User Input
--------------------

You’re probably noticing that a good work flow is to build out the front end, then make it functional, and then connect the wires. Now we’re going to work on capturing the location name using a model and saving it in a database. 

### Local Storage

Ionic has the ability to utilize many storage options. [Local Storage](http://www.w3schools.com/html/html5_webstorage.asp) is the most basic way to store data locally in the browser, since your app is a hybrid app, you can take advatage of this HTML5 feature. [Local Storage](http://www.w3schools.com/html/html5_webstorage.asp) is best for temporary data such as session tokens.

### SQLite

Mobile devices have an embedded SQL database.

### Storage

Ionic has a great [storage service](https://ionicframework.com/docs/v2/storage/) that will automagically use the best availabe storage method. We’ll take advantage of this with SQLite. Install SQLite by running the following command:

`cordova plugin add cordova-sqlite-storage —save`

```

```

`​`​And lets tell Ionic that we’ll be using Storage by importing it to **src/app/app.module.ts and adding it to our `Providers` array: **

```js
import { NgModule } from '@angular/core';
import { IonicApp, IonicModule } from 'ionic-angular';
import { MyApp } from './app.component';

import { Storage } from '@ionic/storage';  // <== add this

import { HomePage } from '../pages/home/home';
import { TodolistPage } from '../pages/todolist-page/todolist-page';

@NgModule({
  declarations: [
    MyApp,
    HomePage,
    TodolistPage
  ],
  imports: [
    IonicModule.forRoot(MyApp)
  ],
  bootstrap: [IonicApp],
  entryComponents: [
    MyApp,
    HomePage,
    TodolistPage
  ],
  providers: [Storage] // <== add this too
})
export class AppModule {}

```









