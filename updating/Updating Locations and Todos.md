Now that we know how to create our locations and todos, lets implement a way to change the names of these items.

### Editing Locations

In our data model in **todolist-model.ts** lets add a `setLocation()` function that takes in a new location name:

```js
setLocation(location): void {
  this.location = location; 
}
```

Now we can use this function in **home.ts** to update a location name:

```js
renameLocationlist(location): void {

    let prompt = this.alertCtrl.create({
      title: 'Rename Location',
      message: 'Enter the new location name',
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

            let index = this.todolists.indexOf(location);

            if (index > -1) {
              this.todolists[index].setLocation(data.location);
            }

          }
        }
      ]
    });
    
    prompt.present(); 
  }
```

This is very similiar to how we created a Location with the only difference being that we set the new title with `setTitle()`​. Implement this function in **home.ts** by adding it to the Edit button**: **

```js
<button ion-button icon-left color="light" (click)="renameLocationlist(todolist)">
  <ion-icon name="clipboard"></ion-icon>
  Edit
</button>
```

Now if you slide a location button to the right and click on the Edit button, a familiar form will appear. Add a new name, hit Save, and you’ll see tha the location name updates. We’re going to do something similiar to update the names of our todos as well. 

First start by adding a `renameTodo()` helper function in our **todolist-model.ts**:

```js
renameTodo(todo, title): void {

  let index = this.todos.indexOf(todo);

  if (index > -1) {
    this.todos[index].title = title; 
  }
}
```

Now we’ll add our form to update the name of the todo in **todolist-page.ts:**

```js
renameTodo(todo): void {

    let prompt = this.alertCtrl.create({
      title: 'Rename Todo',
      message: 'Enter the new Todo name below:',
      inputs: [
        {
          name: 'name'
        }
      ],
      buttons: [
      {
        text: 'Cancel'
      },
      {
        text: 'Save',
        handler: data => {
          this.todolist.renameTodo(todo, data.name)
        }
      }
      ]
    });
    
    prompt.present(); 
  }
```

Now we need to add our function to the front-end in **todolist-page.html:**

```js
<button ion-button icon-left color="light" (click)="renameTodo(todo)">
  <ion-icon name="clipboard"></ion-icon>
    Edit
</button>
```

You should now be able to update location and todo names!







