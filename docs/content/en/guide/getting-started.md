---
title: Getting Started
description: ''
position: 2
category: Guide
---

## Requirements

Make sure you have the newest versions of Nuxt and Firebase installed and setup in your project.

<code-group>
  <code-block label="Yarn" active>

  ```bash
  yarn add nuxt
  yarn add firebase
  ```

  </code-block>
  <code-block label="NPM">

  ```bash
  npm install nuxt
  npm install firebase
  ```

  </code-block>
</code-group>

## Install

Install the module via NPM or Yarn.

<code-group>
  <code-block label="Yarn" active>

  ```bash
  yarn add @nuxtjs/firebase
  ```

  </code-block>
  <code-block label="NPM">

  ```bash
  npm install @nuxtjs/firebase
  ```

  </code-block>
</code-group>

## Configure

Add the below code to your **nuxt.config.js** modules array and adjust it according to your needs.

Visit the [config section](/guide/options/#config) for a detailed overview about each configuration.

### Simple Configuration

```js[nuxt.config.js]
modules: [
    [
      '@nuxtjs/firebase',
      {
        config: {
          apiKey: '<apiKey>',
          authDomain: '<authDomain>',
          databaseURL: '<databaseURL>',
          projectId: '<projectId>',
          storageBucket: '<storageBucket>',
          messagingSenderId: '<messagingSenderId>',
          appId: '<appId>',
          measurementId: '<measurementId>'
        },
        services: {
          auth: true // Just as example. Can be any other service.
        }
      }
    ]
  ],
```

See list of available services [here](/guide/options/#services).

### Full Configuration

If you want to use every little configuration option there is, refer to the example below.

```js[nuxt.config.js]
modules: [
    [
      '@nuxtjs/firebase',
      {
        config: {
          production: {
            apiKey: '<apiKey>',
            authDomain: '<authDomain>',
            databaseURL: '<databaseURL>',
            projectId: '<projectId>',
            storageBucket: '<storageBucket>',
            messagingSenderId: '<messagingSenderId>',
            appId: '<appId>',
            measurementId: '<measurementId>'
          },
          development: {
            apiKey: '<apiKey>',
            authDomain: '<authDomain>',
            databaseURL: '<databaseURL>',
            projectId: '<projectId>',
            storageBucket: '<storageBucket>',
            messagingSenderId: '<messagingSenderId>',
            appId: '<appId>',
            measurementId: '<measurementId>'
          }
        },
        customEnv: false,
        onFirebaseHosting: false,
        services: {
          auth: {
            persistence: 'local',
            initialize: {
              onAuthStateChangedMutation: "SET_AUTH_USER",
              onAuthStateChangedAction: null,
            },
            ssr: {
              // !! NEVER deploy a service account file to github or to a publicly accessible folder on your server !!
              credential: '~/assets/firebase/serviceAccount.json',
              ignorePaths: [
                '/api/',
                /[^/]+/sub-path\//
              ],
              // Experimental Feature, use with caution.
              serverLogin: {
                sessionLifetime: 60 * 60 * 1000, // one hour
                loginDelay: 50 // minimal recommended delay
              }
            }
          },
          firestore: {
            memoryOnly: false // default
          },
          functions: {
            location: 'us-central1', // Default
            emulatorPort: 12345
          },
          storage: true,
          realtimeDb: true,
          performance: true,
          analytics: true,
          remoteConfig: {
            settings: {
              fetchTimeoutMillis: 60000, // Default
              minimumFetchIntervalMillis: 43200000 // Default
            },
            defaultConfig: {
              welcome_message: "Welcome"
            }
          },
          messaging: {
            createServiceWorker: true,
            actions: [
              {
                action: '<randomName>',
                url: '<randomUrl>'
              }
            ],
            fcmPublicVapidKey: '<publicVapidKey>' // OPTIONAL : Sets vapid key for FCM after initialization
          }
        }
      }
    ]
  ],
```

You can also separate the config from the module array by using the **firebase** object:

```js[nuxt.config.js]
modules: ['@nuxtjs/firebase'],

firebase: {
// options
}
```