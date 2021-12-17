
# Angular
> - https://www.tektutorialshub.com/angular-tutorial/
> - https://dev.to/bespoyasov/clean-architecture-on-frontend-4311
> - https://coryrylan.com/blog/angular-form-builder-and-validation-management
> - https://www.tutsmake.com/
> - https://github.com/Procaseycash/ng-pure-datatable
> - http://jsfiddle.net/gavinfoley/fR32K/
> - https://nehalist.io/working-with-models-in-angular/ 
> - https://stackblitz.com/angular/jaamvvovxlme?file=angular.json
> - https://angular.io/guide/i18n
> - https://stackblitz.com/angular/aqnrddojgan?file=src%2Fapp%2Fhero-detail%2Fhero-detail.component.ts
> - https://therichpost.com/how-to-implement-fullcalendar-in-angular-8/
> - https://stackoverflow.com/questions/28339838/how-to-define-different-fonts-for-different-language-using-angularjs-i18n
> - https://www.concretepage.com/angular/angular-formgroup-addcontrol-removecontrol
> - https://medium.com/angular-shots/shot-3-how-to-add-http-headers-to-every-request-in-angular-fab3d10edc26
> - https://dzone.com/articles/how-to-use-async-pipe-in-angular-8
> - https://github.com/bootsoon/ng-circle-progress
> - https://stackblitz.com/edit/ng-circle-progress-demo?file=src%2Fapp%2Fapp.component.html
> - https://malcoded.com/posts/angular-i18n/
> - https://jasonwatmore.com/post/2020/10/07/angular-http-put-request-examples
> - https://www.thirdrocktechkno.com/blog/how-to-implement-localization-in-angular-10/
> - https://pkief.medium.com/angular-desktop-apps-a9ce9e3574e8
> - https://www.logicflow.ai/blog/params/post/2543411/
> - https://www.geeksforgeeks.org/whats-the-difference-between-ng-pristine-and-ng-dirty-in-angularjs/
> - https://newbedev.com/how-to-find-the-invalid-controls-in-angular-4-reactive-form



# Angular 10 - Fix CommonJS or AMD dependencies can cause optimization bailouts
>  When you use a dependency that is packaged with CommonJS, it can result in <a href="https://web.dev/commonjs-larger-bundles/" rel="noreferrer">larger slower applications</a>.Starting with version 10, Angular now warns you when your build pulls in one of these bundles. If you’ve started seeing these warnings for your dependencies, let your dependency know that you’d prefer an ECMAScript module (ESM) bundle.Here is an official documentation - <a href="https://angular.io/guide/build#configuring-commonjs-dependencies" rel="noreferrer">Configuring CommonJS dependencies</a>

In your angular.json file look for the build object and add

```allowedCommonJsDependencies```

as shown below -

```
"build": {
  "builder": "@angular-devkit/build-angular:browser",
  "options": {
     "allowedCommonJsDependencies": [
        "rxjs-compat",
         ... few more commonjs dependencies ... 
     ]
     ...
   }
   ...
},
```

# Angular image src as function return
TS:
```  
    getImage(id){
        return http.get(url/id);
    }
```
HTML:
```
<img [src]="getImage(user.profileImageId)" />
```
# BASE64 to image angular

> Import DomSanitizer:
```
import { DomSanitizer } from '@angular/platform-browser';
```
> define in constructor:
```constructor(private _sanitizer: DomSanitizer) { }
```
> Sanitize the Base64 string you want to pass as your image source (use trustResourceUrl):

```
this.imagePath = this._sanitizer.bypassSecurityTrustResourceUrl('data:image/jpg;base64,' 
                 + toReturnImage.base64string);
```
> Bind to html:

```
<img [src]="imagePath">
```
# 
# Angular FormGroup reset doesn't reset validators

It (FormGroup) behaves correctly. Your form requires username and password, thus when you reset the form it should be invalid (i.e. form with no username/password is not valid).

If I understand correctly, your issue here is why the red errors are not there at the first time you load the page (where the form is ALSO invalid) but pop up when you click the button. This issue is particularly prominent when you're using Material.

AFAIK, <mat-error> check the validity of FormGroupDirective, not FormGroup, and resetting FormGroup does not reset FormGroupDirective. It's a bit inconvenient, but to clear <mat-error> you would need to reset FormGroupDirective as well.

To do that, in your template, define a variable as such:
```
<form [formGroup]="myForm" #formDirective="ngForm" 
  (ngSubmit)="submitForm(myForm, formDirective)">
And in your component class, call formDirective.resetForm():

private submitForm(formData: any, formDirective: FormGroupDirective): void {
    formDirective.resetForm();
    this.myForm.reset();
}
```
> GitHub issue: https://github.com/angular/material2/issues/4190

  
