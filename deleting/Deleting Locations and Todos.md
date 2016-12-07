In order to delete we’ll just need to add a function to **home.ts** to delete locations and **todolist-page.ts** to delete a todo, so lets get to work!

First start by adding the `deleteLocationlist(todolist)` to **home.ts:**

```js
deleteLocationlist(todolist): void {

    let index = this.todolists.indexOf(todolist);

    if (index > -1) {
      this.todolists.splice(index, 1); 
    }
  }
```

And then update our front-end to invoke this function when the delete button is pressed in **home.html:**

```js
<button ion-button icon-left color="danger" (click)="deleteLocationlist(todolist)">
  <ion-icon name="trash"></ion-icon>
  Delete
</button>
```

---

To remove a todo from a location we’ll need to add a helper function to it’s data model in **todolist-model.ts:**

```js
deleteTodo(todo): void {

  let index = this.todos.indexOf(todo);

  if (index > -1) {
    this.todos.splice(index, 1); 
  }
}
```

Now we can simply call this function from **todolist-page.ts** in `removeTodo()`**:**

```js
removeTodo(todo): void {
    this.todolist.deleteTodo(todo);
  }
```

And invoke this function on the front-end in **todolist-page.html:**

```js
<button ion-button icon-left color="danger" (click)="removeTodo(todo)">
  <ion-icon name="trash"></ion-icon>
  Delete
</button>
```

You should now be able to delete a location and a todo!





