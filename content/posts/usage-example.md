---
title: "Usage Example"
date: 2017-11-30T12:57:04+01:00
draft: false
---

Open [Google Cloud Console](https://console.cloud.google.com/) and create a new project (or reuse an existing one).

![Google Cloud Project Creation](/images/Screen Shot 2017-11-30 at 14.06.08.png)

Make sure to enable Billing to be able to use *Cloud Functions*, *Storage* and *Datastore*.

![Enable Cloud Functions](/images/Screen Shot 2017-11-30 at 14.20.23.png)
![Enable Storage](/images/Screen Shot 2017-11-30 at 14.13.39.png)

*Datastore* will be used by the example component to persist data. Make sure to enable it.

![Enable Datastore](/images/Screen Shot 2017-11-30 at 14.26.30.png)

Finally, components.cloud requires that the *Google Cloud Functions API* is enabled as well.

![Enable Datastore](/images/Screen Shot 2017-11-30 at 14.22.02.png)

Google Cloud is now setup to start using Serverless Web Components. We will use a [UpVote Button Component](https://github.com/rkusa/upvote-button-component) as an example.

At first, [download the component](https://github.com/rkusa/upvote-button-component/blob/master/dist/upvote-button.js) and load it in your website. Loading it at the end, just before the `</body>` tag, is fine.

```html
<script src="/upvote-button.js"></script>
```

With the script loaded, we now have a new HTML tag: `<upvote-button>`. The usage of this component requires to set an `endpoint` attribute according to the Google Cloud project set up above. The endpoint should be constructed like `https://{REGION}-{PROJECT_ID}.cloudfunctions.net/` where `{REGION}` should be replace by the Google Cloud region (probably `us-central1` when using Google Cloud Functions) and `{PROJECT_ID}` should be replaced by your Google Cloud's project id. This is currently the only kind of supported endpoint. The goal is to add support for other FaaS providers in the future.

With the attribute set, the component's tag might look like:

```html
<upvote-button endpoint="https://us-central1-components-cloud-website.cloudfunctions.net/"></upvote-button>
```


Since the component's functions aren't deployed, yet, you will see a deploy button at first.

![Deploy Button](/images/Screen Shot 2017-11-30 at 14.45.26.png)

Clicking the deploy button will redirect to the deployment process which prompts for an authorization of the deployment.

![Deployment Authorization](/images/Screen Shot 2017-11-30 at 14.08.17.png)

Authorizing the deployment requires corresponding access to your Google Cloud account.

![Choose an account](/images/Screen Shot 2017-11-30 at 14.12.20.png)

The required OAuth scopes are `https://www.googleapis.com/auth/cloud-platform` (required for creating Google Cloud Functions) and `https://www.googleapis.com/auth/devstorage.read_write` (required to Upload the source of the Cloud function).

![OAuth authorization](/images/Screen Shot 2017-11-30 at 14.12.25.png)

Once access according to those scopes has been granted, the deployment is executed and eventually redirected back to your website. After a successful deployment, the deploy button is replaced by the actual component, as shown below.

![The deployed component](/images/Screen Shot 2017-11-30 at 14.51.07.png)


