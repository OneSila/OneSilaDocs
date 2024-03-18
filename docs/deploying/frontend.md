
## Problem solving

Github only allows a deployment key to be used once.
The way around it is to add the key to one of the user accounts as an ssh-key

(https://docs.github.com/en/authentication/troubleshooting-ssh/error-key-already-in-use)

### Deployment

1. Install NPM

```commandline
sudo apt-get install npm
```

2. We will first need to pull the fontend repository in the same folder as the backend one:

```commandline
cd /home/onesila/
git clone git@github.com:OneSila/OneSilaFrontend.git
```

3. Build the files:

```commandline
cd /home/onesila/OneSilaFrontend
export VITE_APP_API_GRAPHQL_URL=$DEV_API_GRAPHQL_URL
npm install -g npm
npm install
npm run build
```


In order to connect the frontend to the backend, we must add two sections to our nginx file. 

Section 1: direct backend django routes

    replace location / { by:

    location ~ ^/(admin|api|emtools|graphql|pricecards|product_import_export_tools|telegram_chatbot|channable)/ {



Section 2: The new root - everything vue/frontend:

    location / {
        if (-f /home/tim//maintenance.flag) {
            return 503;
        }
        # Frontend files are housed here.

        # Let's keep the browser from caching files the index.html
        # whenever an updates happens - which forces users to hard-refresh.

        location ~* \.html?$ {
            expires -1;
            etag on;
        }

        location ~* \.(css|js)$ {
            access_log off;
            expires max;
        }

        root /home/onesila/OneSilaFrontend/dist/;
        try_files $uri $uri/ /index.html;
    }


### Auto deployment

In our auto deployment screept we will have

```yaml
  script: |
    export VITE_APP_API_GRAPHQL_URL=https://${{ secrets.DEVELOPMENT_HOSTNAME }}/graphql/
    export VITE_APP_API_GRAPHQL_WEBSOCKET_URL=wss://${{ secrets.DEVELOPMENT_HOSTNAME }}/graphql/
    export VITE_APP_SENTRY_DSN=${{ secrets.SENTRY_DSN }} 
    export VITE_APP_SENTRY_ENV=development
```

DEVELOPMENT_HOSTNAME should be already configured in the backend but make sure this secret is added on github.
Also make sure you add VITE_APP_SENTRY_ENV, when we set it to 'development' we will have the apollo cache system disabled by default.