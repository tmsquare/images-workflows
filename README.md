# Cloudflare Workflows

A workflows project with 4 steps:   
 *  1) API call to generate image
 *  2) Store image on R2
 *  3) Log request in D1
 *  4) Send image URL via email

## Prerequisites

 *  Sign up for a Cloudflare Account : `https://dash.cloudflare.com/sign-up`
 *  Install npm: `https://docs.npmjs.com/getting-started`
 *  Install Node.js: `https://nodejs.org/en/`
 *  Install Wrangler within your project using npm and Node.js: `npm install wrangler --save-dev` 

## Usage

* Clone this repository to get started with Workflows
* Read the [Workflows announcement blog](https://blog.cloudflare.com/building-workflows-durable-execution-on-workers/) to learn more about what Workflows is and how to build durable, multi-step applications using the Workflows model.
* Review the [Workflows developer documentation](https://developers.cloudflare.com/workflows/) to dive deeper into the Workflows API and how it works.

**Visit the [get started guide](https://developers.cloudflare.com/workflows/get-started/guide/) for Workflows to create and deploy your first Workflow.**

### Example

You can create a project using this template by using `npm create cloudflare@latest`:

```sh
npm create cloudflare@latest workflows-starter -- --template "cloudflare/workflows-starter"
```

This will automatically clone this repository, install the dependencies, and prompt you to optionally deploy:

```sh
╭ Create an application with Cloudflare Step 1 of 3
│
├ In which directory do you want to create your application?
│ dir ./workflows-tutorial
│
├ What would you like to start with?
│ category Template from a GitHub repo
│
├ What's the url of git repo containing the template you'd like to use?
│ repository cloudflare/workflows-starter
│
├ Cloning template from: cloudflare/workflows-starter
│
├ template cloned and validated
│
├ Copying template files
│ files copied to project directory
│
├ Installing dependencies
│ installed via `npm install`
│
╰ Application created

╭ Configuring your application for Cloudflare Step 2 of 3
│
├ Installing @cloudflare/workers-types
│ installed via npm
│
├ Adding latest types to `tsconfig.json`
│ added @cloudflare/workers-types/2023-07-01
│
├ Do you want to use git for version control?
│ yes git
│
├ Initializing git repo
│ initialized git
│
├ Committing new files
│ git commit
│
╰ Application configured

╭ Deploy with Cloudflare Step 3 of 3
│
├ Do you want to deploy your application?
│ no deploy via `npm run deploy`
│
╰ Done

────────────────────────────────────────────────────────────
🎉  SUCCESS  Application created successfully!
```

The [Workflows documentation](https://developers.cloudflare.com/workflows/) contains examples, the API reference, and architecture guidance.


## Update the code accordingly

### 1. Create a Cloudflare D1 database (from the dashboard)

### 2. Create a Cloudflare R2 bucket (from the dashboard)

### 3. Update the ``wranggler.jsonc`` file and configure the bindings 

```wrangler.jsonc
{
  "name": "images-workflows",
  "main": "src/index.ts",
  "compatibility_date": "2022-07-12",
  "workers_dev": false,
  "observability": true,

  "r2_buckets": [
    {
      "binding": "MY_BUCKET", // 
      "bucket_name": "<YOUR_BUCKET_NAME>"
    }
  ],

  "d1_databases": [
    {
      "binding": "MY_D1", // 
      "database_name": "<YOUR_DATABASE_NAME>"
    }
  ],

}
```

### (optional) 4. Get your OpenAI & Sendgrid API tokens
Set these environment variables for your worker (`CF_ACCOUNT_ID` being your cloudflare account ID)
```sh
$ wrangler secret put OPENAI_API_KEY
$ wrangler secret put SENDGRID_API_KEY
$ wrangler secret put CF_ACCOUNT_ID
```

### 5. Test
Deploy your worker on your local machine to test
```sh
npx wrangler dev
```

### 6. Deployment
Deploy your worker on Cloudflare Edge
```sh
npx wrangler deploy
```