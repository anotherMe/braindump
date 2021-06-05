
# Angular

These are actually just a bunch of sparse notes taken during the Udemy course [Angular - The complete guide](https://www.udemy.com/course/the-complete-guide-to-angular-2).


### Strict mode

Angular CLI creates all new workspaces and projects with *strict mode* enabled.

You can apply these settings at the workspace and project level.

**Note about the Udemy course**: all the course code will only work if you are NOT using *strict mode*. If you enabled it by accident, you can also disable it by setting `strict: false ` in your **tsconfig.json** file.


### Bootstrap setup

To add bootstrap on an existing project:

```
npm install bootstrap
npm install @popper/core
```

Then modify the **angular.json** file to add a reference to bootstrap files:

```json
...
"styles": [
    "node_modules/bootstrap/dist/css/bootstrap.min.css",
    ...
],
"scripts": [
    "node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"
]
...
```

### Add routing to existing project

Just refer to [this](https://www.samjulien.com/add-routing-existing-angular-project) article.

Also the [Tour of Hero tutorial project](https://angular.io/tutorial/toh-pt5) could help.