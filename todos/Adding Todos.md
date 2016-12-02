Now that we are able to add locations, lets replace our hardcoded todos in a smiliar manner.

Update **todolist-page.ts** to reflect the following:

```js
import { Component } from '@angular/core';
import { NavController, NavParams, AlertController } from 'ionic-angular';

@Component({
  selector: 'todolist-page',
  templateUrl: 'todolist-page.html'
})

export class TodolistPage {

  checklist: any; 

  constructor(public navCtrl: NavController, public navParams: NavParams, public alertCtrl: AlertController) {
    this.checklist = this.navParams.get('todolist');
  }

}
```

We import [NavParams](http://ionicframework.com/docs/v2/api/navigation/NavParams/) so we can access our Todolist data (need to expand). We then set checklist as a class variable and then access our `todolist` from navParams and save it as `checklist`.