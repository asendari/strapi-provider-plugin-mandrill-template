# Strapi Mandrill plugin

Mandrill plugin for Strapi 4 with support template

## Installation

```sh
npm install strapi-provider-plugin-mandrill-template
```

or

```sh
yarn add strapi-provider-plugin-mandrill-template
```


## Dependencies

We are using `@mailchimp/mailchimp_transactional` package. 

So for all send message we'll use this post: https://mailchimp.com/developer/transactional/api/messages/

## Add Pluggin

Add on config/plugins.js file the configuration bellow

```
  email: {
    config: {
      provider: "strapi-provider-plugin-mandrill-template",
      providerOptions: {
        apiKey: env('MANDRILL_API_KEY'),
      },
     settings: {
        defaultFrom: env('MANDRILL_FROM_EMAIL'),
        defaultName: env('MANDRILL_FROM_NAME'),
        defaultReplyTo: env('MANDRILL_FROM_EMAIL')
      },
    },
  }
```

## Use template with Merge Vars

```
  await strapi.plugins['email'].services.email.send({
    to: 'test@mail.com',
    from: 'test@mail.com',
    subject: 'Strapi mail with template and global merge vars',
    template_name: 'mailchimp-template-name',
    global_merge_vars: [
      { name: 'firstname', content:'Thomas' }
    ]
  })
```

## Use template with Handlebars

```
  await strapi.plugins['email'].services.email.send({
    to: 'test@mail.com',
    from: 'test@mail.com',
    subject: 'Strapi mail with template and handlebars formating',
    template_name: 'mailchimp-template-name',
    merge_language: 'handlebars',
    global_merge_vars: [
      { name: 'firstname', content:'Thomas' }
    ]
  })
```