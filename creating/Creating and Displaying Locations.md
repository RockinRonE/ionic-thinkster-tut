Adding a New Location Form
--------------------------

**In home.html l**ets start by building out our `add-circle` button at the upper right-hand corner on our Location list page. We’ll be taking advantage of Ionic’s [AlertController](http://ionicframework.com/docs/v2/api/components/alert/AlertController/) to take in the location name of our todo list. To do this we’ll first have to import it in **home.ts** by adding **AlertController** to the import line of ‘ionic-angular' :

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

---

Capturing and Displaying Location Data
--------------------------------------

Currently our app shows a location and a todo that is hard coded. Before we get into how to make this dynamic we should think about how we want our todo list data modeled. Since Ionic does not have a model generator we’ll have to create it ourselves. 

Lets get started by creating a new directory inside **src** called **models. **

**
**

Then create a file called **todolist-model.ts** in this directory like so:

![Screen Shot 2016-12-01 at 3.54.02 PM.png](resources/86219DBCBC00715C263CDAC24038046C.png)

Update **todolist-model.ts** to the following:

```js
export class TodolistModel {
    
    constructor(public location: string, public items: any[]) {
       
    }

}
```

Our todolist model is sparse for the moment but we’ll build it out soon. 

Now we need to capture the location that the user enters in our form and display it on our homepage. To capture the user input, update the handler in `addLocationlist()` in **home.ts **to the following:

```js
export class HomePage {

  todolists: TodolistModel[] = [];

  constructor(public navCtrl: NavController, public alertCtrl: AlertController) {
    
  }

  viewTodolist(todolist): void {
    this.navCtrl.push(TodolistPage, {
      todolist: todolist
    });
  }

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
            
            let newTodolist = new TodolistModel(data.location, []);
            this.todolists.push(newTodolist);

            console.log('Data saved!');
          }
        }
      ]
    });
    prompt.present(); 
  }

}
```

Here we instantiate a new `TodolistModel` with `data.location` as it’s location and an empty array and save it as `newTodolist`. We then push this to `todolists`​, which is now declared at the top of our class (on line 3) which makes it accessible throughout by using `this`​. Now that this is setup we need to display it on our front-end in **home.html. **

Update `ion-item-sliding` in **home.html** to the following:

```js
<ion-item-sliding *ngFor="let todolist of todolists">

      <button ion-item (click)="viewTodolist(todolist)">
        {{todolist.location }}
        <span>{{todolist.todos.length}} todos</span>
      </button>
      
........
```

We added [\*ngFor](https://angular.io/docs/ts/latest/api/common/index/NgFor-directive.html) to iterate over our todolists as a todolist (help?). Then we replace our text with `{{ todolist.location }}` to display the location from the user and `{{ todolist.items.length }}`​ to display the count of any todos for our list. You should now be able to enter a new location, hit Save, and it will appear on **home.html**

**
**

![out.gif](resources/04E58D6415EC48B52BE66EB12F0D5B42.gif)





---













