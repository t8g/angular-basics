---
theme: ./theme
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Lucca Angular for integrator training slides
drawings:
  persist: false
title: Angular Basics
---

# Angular Basics

Formation Angular pour les intégrateurs

---
layout: section
---

# Component <small>1/2</small>

Création d'un component

Par convention, on utilise UN fichier contenant UNE classe pour UN Component.

<div class="center">1 component = 1 classe dans 1 fichier</div>

Convention de nommage : `something.component.ts`

Angular expose ses classes, méthodes et outils dans le namespace `@angular`. Par exemple `@angular/core`.

L'api complète exposée est présentée ici : [API Angular](https://angular.io/api)

Pour créer un **Component** il faut exposer une classe décorée par `@Component`. En passant les options suivantes :

* `selector` : string nom de l'élément html créé permettant d'utiliser le component.
* `template` : string code html du Component

---
layout: section
---

# Component <small>2/2</small>

Utilisation d'un Component

Pour utiliser un Component dans un autre, il faut le déclarer dans le Module.

`declarations`: any[] liste des Components utilisés

```ts
@NgModule({
  ...
  declarations: [ MyComponent ],
  ...
})
```

Le nouveau Component pourra alors être utilisé dans l'ensemble du Module.

Ne pas oublier d'importer le Component (ici `PlanetsComponents`) avec le chemin relatif et sans l'extension '.ts'.

---
layout: section
---

# Template

Afficher les propriétés d'un Component

Dans la classe, on ajoute un attribut à la classe.

```ts
export class PlanetsComponent {
    title = 'La liste des planètes'
}
```

Dans le template, on affiche une propriété de l'objet Component en utilisant les 'doubles moustaches' `{{ title }}`

```html
<h2>{{ title }}</h2>
```

---
layout: section
---

# Property Binding <small>1/3</small>

Syntaxe

```ts
[prop]="value"
```

*One way data binding*

Les changements sur les propriétés faites dans le component sont actualisés sur le DOM, mais pas l'inverse.

---
layout: section
---

# Property Binding <small>2/3</small>

Différence attribut - propriété

```html
<a href='foo.html' class='test one' name='fooAnchor' id='fooAnchor'>Hi</a>
```

```
+-------------------------------------------+
| a                                         |
+-------------------------------------------+
| href:       "http://example.com/foo.html" |
| name:       "fooAnchor"                   |
| id:         "fooAnchor"                   |
| className:  "test one"                    |
| attributes:                               |
|    href:  "foo.html"                      |
|    name:  "fooAnchor"                     |
|    id:    "fooAnchor"                     |
|    class: "test one"                      |
+-------------------------------------------+
```

```
const link = document.getElementById('fooAnchor');
alert(link.href);                 // alerts "http://example.com/foo.html"
alert(link.getAttribute("href")); // alerts "foo.html"
```

---
layout: section
---

# Property Binding <small>3/3</small>

Attribute binding

Il peut arriver que l'on veuille adresser un attribut et non pas une propriété.

```
<table>
    <tr>
        <td>un</td>
        <td>deux</td>
    </tr>
    <tr>
        <td [attr.colspan]="1 + 1">trois</td>
    </tr>
</table>
```

---
layout: section
---

# Class Binding

Ajout de classes css dynamquement

```html
<span class="un deux" [class]="myClass">Test</span>
```

Attention la classe est écrasée

```html
<span [class.un]="true" [class.deux]="false">Test</span>
```

```html
<span [ngClass]="{un: true, deux: false}"></span>
```

---
layout: section
---

# Style Binding

Modification dynamique de styles inline

```html
<p [style.color]="pinkColor">
    [style.color]="pinkColor"
</p>

<p [style.fontSize.em]="1.5">
    [style.fontSize.em]="1.5"
</p>
```

---
layout: section
---

# Event Binding

Déclenchement d'actions sur des événements

```html
<button (click)="doSomething()">un</button>
<button on-click="doSomething()">deux</button>
```

Où `doSomething` est une méthode du component.

Depuis le template, on peut passer l'objet Event `$event` à la méthode utilisée.

```html
<button (click)="doSomething($event)">un</button>
```

Il est alors possible d'utiliser. (Par exemple `$event.stopPropagation`).

---
layout: section
---

# Input Properties <small>1/2</small>

Déclaration via Decorator

Importer le Decorator Input 
```ts
import { Input } from '@angular/core';
```

Ajouter `Input()` devant la propriété
```ts
@Input() name = '';
```

---
layout: section
---

# Input Properties <small>2/2</small>

Utilisation


```html
<my-component [name]="'John Doe'"></my-component>
```

---
layout: section
---

# Output Properties <small>1/4</small>

Mise en place de l'event

Importer EventEmitter 

```ts
import { EventEmitter } from '@angular/core';
```

Déclarer l'event dans la classe

```ts
change = new EventEmitter();
```

---
layout: section
---

# Output Properties <small>2/4</small>

Déclaration via Decorator

Importer le Decorator Output

```ts
import { Output } from '@angular/core';
```

Ajouter `Output()` devant l'event 
```ts
@Output() change = new EventEmitter();
```

---
layout: section
---

# Output Properties <small>3/4</small>

Déclenchement de l'event

Où désiré dans le code, il suffit d'appeler : 

```ts
this.change.emit(data);
```

Avec **data** l'information à transmettre.

---
layout: section
---

# Output Properties <small>4/4</small>

Utilisation

Comme un event natif : 

```html
<my-component (change)="doSomething($event)">
```

et on récupère les informations dans **$event**


---
layout: section
---

# Built-in Directives <small>1/3</small>

ngIf

```html
<div *ngIf="errorCount > 0" class="error">
  {{errorCount}} errors detected
</div>
```

---
layout: section
---

# Built-in Directives <small>2/3</small>

ngSwitch

```html
<div [ngSwitch]="value">
    <p *ngSwitchCase="'init'">increment to start</p>
    <p *ngSwitchCase="0">0, increment again</p>
    <p *ngSwitchCase="1">1, increment again</p>
    <p *ngSwitchCase="2">2, stop incrementing</p>
    <p *ngSwitchDefault>&gt; 2, STOP!</p>
</div>
```

---
layout: section
---

# Built-in Directives <small>3/3</small>

ngFor (ngForOf)

```html
<li *ngFor="let planet of planets; let i = index">
    {{ i }} : {{ planet }}
</li>
```

En plus de `index`, on a : `first`, `last`, `even`, `odd`

---
layout: section
---

# Pipes

Transformation de données à l'affichage

```html
{{ valeur_à_formater | nom_du_pipe }}
{{ valeur_à_formater | nom_du_pipe:argument_1:argument_2 }}
{{ valeur_à_formater | nom_du_pipe_1 | nom_du_pipe_2 }}
```

*Quelques pipes fournies par Angular*

AsyncPipe, CurrencyPipe, DatePipe, DecimalPipe, I18nPluralPipe, I18nSelectPipe, JsonPipe, LowerCasePipe, PercentPipe, SlicePipe, TitleCasePipe, UpperCasePipe

---
layout: section
---

# Custom Pipes

Écrire ses propres Pipes

something.pipe.ts
```ts
import { Pipe, PipeTransform } from	'@angular/core'

@Pipe({ name: 'summary' })
export class SomethingPipe implements PipeTransform {
  transform (value: string, param1) {
    // code
  }
}
```

Déclaration dans le module
```ts
@NgModule({
    ...
    declarations: [SomethingPipe]
    ...
})
```

---
layout: section
---

# Elvis Operator

Safe navigation operator

permet d'éviter les erreurs dûes à la lecture de propriétés sur les objets null ou undefined.

```html
Provoque une erreur si user n'existe pas
{{ user.firstName }}

Sans erreur (n'affiche rien) si user n'existe pas
{{ user?.firstName }}
```

---
layout: section
---

# Transclusion

Transporter le contenu d'un Component

Le système de **transclusion** de Angular. Il suffit d'utiliser le component `<ng-content>` pour récupérer le contenu passé.

Il est possible de récupérer un sous contenu en précisant la cible via l'attribut `select` de ce component. Le ciblage se fait alors avec un sélecteur css.

---
layout: section
---

# Forms

Model Driven Forms vs Template Driven Forms

Une approche entièrement déclarative, reposant sur des directives. C'est l'approche **Template Driven**.

Une approche plus programatique, dans laquelle il est de la responsabilité du développeur de créer le modèle. C'est l'approche **Model Driven**

---
layout: section
---

# ReactiveForms  <small>1/13</small>

Préparation

```ts
import { ReactiveFormsModule } from '@angular/forms';

@NgModule({
  imports: [
    ReactiveFormsModule
  ]
});
```


---
layout: section
---

# ReactiveForms  <small>2/13</small>

FormGroup

Pour représenter et manipuler le formulaire, nous allons créer un objet `FormGroup`.

```ts
import { FormGroup } from '@angular/forms';

export class UserFormComponent implements OnInit {

  form: FormGroup;

  ngOnInit() {
    this.form = new FormGroup({});
  }

}
```

---
layout: section
---

# ReactiveForms  <small>3/13</small>

FormControl

Un formulaire n'est intéressant que s'il contient des champs.

```ts
import { FormGroup, FormControl } from '@angular/forms';

export class UserFormComponent implements OnInit {

  form: FormGroup;

  ngOnInit() {
    this.form = new FormGroup({
      name: new FormControl()
    });
  }

}
```

---
layout: section
---

# ReactiveForms  <small>4/13</small>

Sous groupes

Il est possible de déclarer un `FormGroup` dans un `FormGroup`.

```ts
import { FormGroup, FormControl } from '@angular/forms';

export class UserFormComponent implements OnInit {

  form: FormGroup;

  ngOnInit() {
    this.form = new FormGroup({
      address: new FormGroup({
          street: new FormControl()
      })
    });
  }

}
```

---
layout: section
---

# ReactiveForms  <small>5/13</small>

Bound to Html

```html
<form [formGroup]="form">
  <input formControlName="name" type="text">
  <fieldset formGroupName="address">
      <input formControlName="street" type="text">
  </fieldset>
</form>
```

---
layout: section
---

# ReactiveForms  <small>6/13</small>

Validators

Un `FormControl` peut être construit avec :

1. une valeur par défaut,
2. un validateur ou un tableau de validateurs.

```ts
import { Validators } from '@angular/forms';

export class UserFormComponent implements OnInit {
  ngOnInit() {

    this.form = new FormGroup({
      name: new FormControl('', Validators.required),
      bio: new FormControl('', [
        Validators.required,
        Validators.minLength(10)
      ]),
    });

  }

}
```

---
layout: section
---

# ReactiveForms  <small>7/13</small>

Builtin validators

* Validators.required
* Validators.minLength(n: number)
* Validators.maxLength(n: number)
* Validators.pattern(r: Regexp)
* Validators.min(n: number)
* Validators.max(n: number)
* Validators.email
* Validators.requiredTrue

---
layout: section
---

# ReactiveForms  <small>8/13</small>

State

Un objet `FormControl` (et donc `FormGroup`) porte un état.

```ts
this.form = new FormGroup({
    name: new FormControl('', Validators.required),
});


this.form.touched; // true / false
this.form.get('name').touched; // true / false
```

Les propriétés d'états :

<div style="display:flex;flex-direction:column">
  <ul>
    <li>valid / invalid</li>
    <li>dirty / pristine</li>
    <li>touched / untouched</li>
  </ul>
  <ul>
   <li>value</li>
  </ul>
</div>

---
layout: section
---

# ReactiveForms  <small>9/13</small>

Error message & error class

```html
<label for="name" class="six columns-md" [class.text-danger]="form.get('name').touched && form.get('name').invalid">
    Name
    <input 
        formControlName="name" 
        id="name" 
        type="text" 
        [class.has-error]="form.get('name').touched && form.get('name').invalid" 
        class="u-full-width">
    <p *ngIf="form.get('name').touched && form.get('name').invalid" class="text-danger">Required</p>
</label>
```

---
layout: section
---

# ReactiveForms  <small>10/13</small>

Errors messages : Shortcuts

```ts
  form = new FormGroup({
    one: new FormControl(undefined, [Validators.required]),
    two: new FormGroup({
      three: new FormControl(),
    }),
  });

  oneControl = this.form.get('one') as FormControl;
  threeControl = this.form.get('two.three') as FormControl;
```

```html
<label for="name" class="six columns-md" [class.text-danger]="oneControl.touched && oneControl.invalid">
    One
    <input [class.has-error]="oneControl.touched && oneControl.invalid"
      formControlName="one" id="one" type="text" class="u-full-width">
    <p *ngIf="oneControl.touched && oneControl.invalid" class="text-danger">Required</p>
</label>
```

---
layout: section
---

# ReactiveForms  <small>11/13</small>

Erreurs spécifiques

La propriété `errors` d'un `FormControl` contient des informations sur les erreurs.

```html
<div class="row">
    <label for="bio" class="twelve columns-md" [class.text-danger]="bio.touched && bio.invalid">
        Bio
        <textarea [class.has-error]="bio.touched && bio.invalid" 
          formControlName="bio" id="bio" class="u-full-width"></textarea>
        <p *ngIf="bio.touched && bio.invalid && bio.errors['required']" class="text-danger">Required</p>
        <p *ngIf="bio.touched && bio.invalid && bio.errors['minlength']" class="text-danger">
            Minlength : {{ bio.errors['minlength'].actualLength }} / {{ bio.errors['minlength'].requiredLength }}
        </p>
    </label>
</div>
```

---
layout: section
---

# ReactiveForms  <small>12/13</small>

Valeurs initiales d'un formulaire

```ts
// remplit les champs en commun
this.form.patchValue({ name: 'John' });
// remplit tout (mais ne support pas les manques)
this.form.setValue({
  name: 'John',
  email: 'john@doe.fr',
});
```

---
layout: section
---

# ReactiveForms  <small>13/13</small>

Soumettre le formulaire

Pour soumettre le formulaire on utilise l'event `submit`.

```html
<form [formGroup]="form" novalidate (submit)="saveUser()">
...
</form>
```

---
layout: section
---

# Template Drive Forms <small>1/8</small>

Déclaration

`NgForm` est un directive dont le selecteur est  `<form>`. De plus l'instance de la directive est exposée sous le nom 'ngForm'.

```html
<form #form="ngForm">
</form>
```

Un `NgForm` contient une propriété `form` de type `FormGroup`.

Extrait des sources de Angular.

```ts
this.form = new FormGroup({}, composeValidators(validators), composeAsyncValidators(asyncValidators));
```

---
layout: section
---

# Template Driven Forms <small>2/8</small>

Links to controls

## ngModel

La directive `ngForm` ne créé pas automatiquement les contrôles en lien avec les input. Il faut créer ce contrôle. C'est le rôle de la directive `ngModel`. Qui agit comme `ngForm` mais au niveau d'un input.

## Name

La directive `ngModel` utilisée comme enfant de la directive `ngForm` a besoin d'être liée à celle-ci. Ce lien se fait via l'attribut *name*.

```html
<form #form="ngForm">
    <input ngModel name="username" type="text">
</form>
```

---
layout: section
---

# Template Driven Forms <small>3/8</small>

Links to groups of controls

Il est possible de définir un sous formulaire (fieldset), grâce à la directive `ngModelGroup`.

```html
<form #form="ngForm">

    <input ngModel name="username" type="text">

    <div ngModelGroup="profile">
        <input ngModel name="firstname" type="text">
        <input ngModel name="lastname" type="text">
    </div>

</form>
```

---
layout: section
---

# Template Driven Forms <small>4/8</small>

Valeur initiales

Pour fournir une valeur initiale à un contrôle, on ne peut pas utiliser l'attribut `value`. Celui-ci est écrasé par la directive `ngModel`.
La solution consiste à passer une valeur à cette directive.

```ts
export class UserFormComponent {
  username: string = 't8g';
}
```

```html
<input [ngModel]="username" name="username" id="username" type="text" class="u-full-width">
```

Par contre si on observe la propriété `username`, on s'aperçoit que celle-ci n'est pas mise à jour lorsque la valeur du contrôle change.

---
layout: section
---

# Template Driven Forms <small>5/8</small>

2way data binding : "banana box"

```html
<input [(ngModel)]="username" name="username" id="username" type="text" class="u-full-width">
```

Cette syntaxe est en fait un raccourci pour

```html
<input [ngModel]="username" (ngModelChange)="username = $event" 
  name="username" id="username" type="text" class="u-full-width">
```

---
layout: section
---

# Template Driven Forms <small>6/8</small>

Validation

Dans l'approche Template Driven, la validation se définit grâce à des directives.

```html
<!-- email -->
<input type="email" name="email" ngModel email>
<input type="email" name="email" ngModel email="true">
<input type="email" name="email" ngModel [email]="true">

<!-- minlength / maxlength -->
<textarea name="bio" ngModel maxlength="100">
<textarea name="bio" ngModel [minlength]="min"><!-- min propriété du component -->

<!-- pattern -->
<input type="text" name="username" ngModel pattern="[a-zA-Z ]*">

<!-- required -->
<input type="text" name="username" ngModel required>
```

---
layout: section
---

# Template Driven Forms <small>7/8</small>

Afficher les erreurs

Pour accèder à un `FormControl` en particulier et ainsi à son état, on utilise `form.controls['controlName']`.
Mais attention, à l'initialisation du template, celui-ci est nul. Donc penser à utiliser un *elvis operator*.

```html
<form #form="ngForm">

    <div class="row">
      
      <label for="name" class="six columns-md" 
        [class.text-danger]="form.controls['name']?.touched && form.controls['name']?.invalid">
        Name
        <input ngModel name="name" required 
          [class.has-error]="form.controls['name']?.touched && form.controls['name']?.invalid" 
          id="name" type="text" class="u-full-width">
        <p *ngIf="form.controls['name']?.touched && form.controls['name']?.invalid" class="text-danger">Required</p>
      </label>

    </div>

</form>
```

---
layout: section
---

# Template Driven Forms <small>8/8</small>

Afficher les erreurs : raccourci

Pour alléger un peu le template, il est possible de récupérer une variable locale au template contenant l'instance du `NgModel` et donc l'état du `NgControl` associé.

```html
<form #form="ngForm">

    <div class="row">
      
      <label for="name" class="six columns-md" 
        [class.text-danger]="name.touched && name.invalid">
        Name
        <input ngModel name="name" required #name="ngModel"
          [class.has-error]="name.touched && name.invalid" 
          id="name" type="text" class="u-full-width">
        <p *ngIf="name.touched && name.invalid" class="text-danger">Required</p>
      </label>

    </div>

</form>
```

---
layout: section
---

# Routing <small>1/4</small>

Configuration : ```app.routing.ts```

```ts
import { Routes, RouterModule }   from '@angular/router';
import { FirstComponent } from './first.component';
import { SecondComponent } from './second.component';

// Configuration des routes
const appRoutes: Routes = [
  {
    path: 'first', // url (sans / initial)
    component: FirstComponent // composant à charger pour cette route
  },
  {
    path: 'second',
    component: SecondComponent
  }
];

// Export du module de routing configuré
export const routing = RouterModule.forRoot(appRoutes);
```

---
layout: section
---

# Routing <small>2/4</small>

Intégration dans le module

```ts
import { routing } from './app.routing';
import { AppComponent }  from './app.component';

@NgModule({
  imports: [
    BrowserModule,
    routing
  ],
  declarations: [
    AppComponent
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```

---
layout: section
---

# Routing <small>3/4</small>

Layout

Enfin dans le template du component principal, nous plaçons le component de route : **Router Outlet**

```html
<router-outlet></router-outlet>
```

---
layout: section
---

# Routing <small>4/4</small>

Navigation

Pour naviguer d'une vue à une autre, on utilise une directive ```routerLink``` qui va créer le lien pour nous.

```html
<a routerLink="/first">First</a>
```

**Bonus** : classe active

Il est possible de définir une classe css lorsque la route est active.

```html
<a routerLink="/first" routerLinkActive="active">First</a>
```

---
layout: section
---

# JS : données <small>1/4</small>

forEach : une action pour chaque item

```js
const innerPlanets = [
  { name: 'Mercure', satellites: [] },
  { name: 'Venus', satellites: [] },
  { name: 'Earth', satellites: [{ name: 'Lune' }] },
  { name: 'Mars', satellites: [{ name: 'Phobos' }, { name: 'Déimos' }]},
];

innerPlanets.forEach((planet) => {
  console.log('palnet name', planet.name);
});
```

---
layout: section
---

# JS : données <small>2/4</small>

map : nouveau tableau de données transformées

```js
const planetsNames = innerPlanets.map((planet) => {
  return planet.name;
});
// ou
const planetsNames = innerPlanets.map((planet) => planet.name);
// ou
const planetsNames = innerPlanets.map(({ name }) => name);
```
---
layout: section
---

# JS : données <small>3/4</small>

filter : portion de tableau

```js
const planetsWithSatellites = innerPlanets.filter((planet) => {
  return planet.satellites.length > 0; 
});
// ou
const planetsWithSatellites = innerPlanets.map((planet) => planet.satellites.length > 0);
// ou
const planetsWithSatellites = innerPlanets.map(({ satellites }) => satellites.length > 0);
```

---
layout: section
---

# JS : données <small>4/4</small>

reduce : transformation

```js
const totalNumberOfSatellites = innerPlanets.reduce(
  (acc, planet) => {
    return acc + planet.satellites.length; 
  },
  0
);
```

---
layout: section
---

# Reactive Programming

Définition

>  La programmation réactive est un paradigme de programmation visant à conserver une cohérence d'ensemble en propageant les modifications d'une source réactive (modification d'une variable, entrée utilisateur, etc.) aux éléments dépendants de cette source. - wikipédia

Beaucoup d'outils pour manipuler des données (.map, .filter, .reduce). Mais pour des données qui s'accumulent avec le temps ?

<p class="sub-section">Nouvelle définition</p>

>  "Reactive programming is programming with asynchronous data streams." - André Staltz

---
layout: section
---

# Flux

Définitions

Un **flux** est simplement une collection qui s'étoffe avec le temps

Un **Observable** est un objet encapsulant un flux et qui peut être manipulé comme une collection.

---
layout: section
---

# RxJS <small>1/2</small>

Subscribe & Unsubscribe

```ts
someObservable$.subscribe((value) => {
  console.log('value', value);
});

const observer = {
  next: (value) => console.log('new value', value),
  error: (error) => console.log('error', error),
  complete: () => console.log('end'),
};

someObservable$.subscribe(observer);

const subscription = someObservable$.subscribe(x => console.log(x));
// Plus tard
subscription.unsubscribe();
```

---
layout: section
---

# RxJS <small>2/2</small>

Operators

```ts
// timer$ est un Observable qui compte les secondes 1, 2, 3, ...

timer$.pipe(
  filter((t) => t % 2 === 0),
  map((t) => `Il s'est passé ${t} secondes`),
);
```
