# meteor-issue-3078

Reproduction for https://github.com/meteor/meteor/issues/3078.

## Prerequisites

You must have a local copy of nginx installed.

## Reproduction Steps

1) `git clone https://github.com/hwillson/meteor-issue-3078.git app1`
2) `cd app1`
3) `meteor npm i`
4) `ROOT_URL=http://localhost/app1 meteor --port 3100`

In a separate terminal window:

5) `git clone https://github.com/hwillson/meteor-issue-3078.git app2`
6) `cd app2`
7) `meteor npm i`
8) `ROOT_URL=http://localhost/app2 meteor --port 3200`

In a separate terminal window:

9) sudo nginx -c /path/to/app/app1/nginx.conf

10) Access http://localhost/app1; in your browser console, run:
```js
Meteor._localStorage.setItem('key', 'Some Value!');
```

11) Access http://localhost/app2; in your browser console, run:
```js
Meteor._localStorage.removeItem('key');
```

12) Access http://localhost/app1; in your browser console, run:
```js
Meteor._localStorage.getItem('key');
```

The item will be removed even though we're using 2 separate applications.
