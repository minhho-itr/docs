## Create a new Angular app

Use the [Angular CLI](https://github.com/angular/angular-cli) to bootstrap a new Angular app:

```bash
npm install -g @angular/cli
ng new amplify-app
cd amplify-app
```

### Angular 6+ Support

Currently, the newest versions of Angular (6+) do not include shims for 'global' or 'process' as provided in previous versions. Add the following to your `polyfills.ts` file to recreate them: 

```javascript
(window as any).global = window;
(window as any).process = {
  env: { DEBUG: undefined },
};
``` 

## Create a new Amplify backend

Now that we have a running Angular app, it's time to set up Amplify for this app so that we can create the necessary backend services needed to support the app. From the root of the project, run:

```bash
amplify init
```

When you initialize Amplify you'll be prompted for some information about the app.  For newer versions of Angular, you will have to change the Distribution Directory Path from `dist` to `dist/amplify-app` to match how Angular will build your project.

```console
Enter a name for the project (amplifyapp)

# All AWS services you provision for your app are grouped into an "environment"
# A common naming convention is dev, staging, and production
Enter a name for the environment (dev)

# Sometimes the CLI will prompt you to edit a file, it will use this editor to open those files.
Choose your default editor

# Amplify supports JavaScript (Web & React Native), iOS, and Android apps
Choose the type of app that you're building (javascript)

What JavaScript framework are you using (angular)

Source directory path (src)

Distribution directory path (dist)
Change from dist to dist/amplify-app

Build command (npm run-script build)

Start command (ng serve)

# This is the profile you created with the `amplify configure` command in the introduction step.
Do you want to use an AWS profile
```

When you initialize a new Amplify project, a few things happen:

- It creates a top level directory called `amplify` that stores your backend definition. During the tutorial you'll add capabilities such as authentication, GraphQL API, storage, and set up authorization rules for the API. As you add features, the `amplify` folder will grow with infrastructure-as-code templates that define your backend stack. Infrastructure-as-code is a best practice way to create a replicable backend stack.
- It creates a file called `aws-exports.js` in the `src` directory that holds all the configuration for the services you create with Amplify. This is how the Amplify client is able to get the necessary information about your backend services.
- It modifies the `.gitignore` file, adding some generated files to the ignore list.
- A cloud project is created for you in the AWS Amplify Console that can be accessed by running `amplify console`. The Console provides a list of backend environments, deep links to provisioned resources per Amplify category, status of recent deployments, and instructions on how to promote, clone, pull, and delete backend resources.

## Install Amplify libraries

Inside the app directory, install the Amplify Angular library and run your app:

```bash
npm install --save aws-amplify @aws-amplify/ui-angular
ng serve
```

The `@aws-amplify/ui-angular` package is a set of Angular components and an Angular provider which helps integrate your application with the AWS-Amplify library.  It supports Angular 5.0 and above.  It also includes a [supplemental module](#ionic-4-components) for Ionic-specific components.

<amplify-callout>Angular CLI output warnings: if you see CommonJS or AMD dependencies optimization bailouts warnings using Angular +9 you can use this [gist](https://gist.github.com/gsans/8982c126c4fef668c094ff288f04241b) to remove them. More details about these [here](https://angular.io/guide/build#configuring-commonjs-dependencies).
</amplify-callout>

### Importing the Amplify Angular UI Module

Add the **Amplify Angular UI Module** to `src/app/app.module.ts`:

```ts
import { AmplifyUIAngularModule } from '@aws-amplify/ui-angular';

@NgModule({
  imports: [
    AmplifyUIAngularModule
  ],
});
```
