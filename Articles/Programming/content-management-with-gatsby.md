
Content Management with Gatsby, Contentful & Netlify
===

I’ve been using Gatsby for the better part of 6 months and it’s quickly become my go-to for building static sites. The advantages are huge. You get:

-   A lot of configuration and boilerplate done out of the box.
-   Speed, SEO and performance optimizations.
-   A great community, great docs and a growing plugin ecosystem.
-   And my personal favourite — getting to write all the React & GraphQL code I want.

It’s been a great developer experience, to say the least. However, when building static sites, one of the major concerns in choosing a tool is how content gets updated on the site. Lots of older platforms have solved this one way or another, Wordpress being the most popular of them, but using the triple threat of Gatsby, Netlify, and Contentful, we can build a pretty good alternative to the traditional CMS tools out there while retaining our SEO compatibility.

This article will show you how you can set up a system for managing content on any page of your Gatsby site. In our case, we’ll be using Gatsby’s powerful  `gatsby-node`  API to pull in content from Contentful and to dynamically generate pages. You can also use Contentful data on any existing page via the provided  `graphql`  queries.

This is going to be a long one, so stretch your legs, grab a coffee or pick-me-up of your choice and let’s begin.

You’ll need the  `gatsby-cli`  tool to get started. Run  `npm i -g gatsby`  in your terminal and once that has run, create a new project with

$ gatsby new gatsby-contentul-blog

This will create a new Gatsby project in a folder called  `gatsby-contentful-blog`.  `cd`  into the new project and run  `gatsby develop`. Now you have the default Gatsby starter homepage:

![](https://miro.medium.com/max/30/1*NbgvljiIhmEl8MfiyW1Vhw.png?q=20)

![](https://miro.medium.com/max/1440/1*NbgvljiIhmEl8MfiyW1Vhw.png)

Open up the project in your favourite text editor and navigate to the  `pages`  folder. Let's tweak some of the content in the  `index.js`: (You can just copy and paste this in)

import React from "react";  
import { Link } from "gatsby";import Layout from "../components/layout";  
import Image from "../components/image";  
import SEO from "../components/seo";  
import "./index.css";const IndexPage = () => (  
  <Layout>  
    <SEO title="Home" keywords={[`gatsby`, `application`, `react`]} />  
    <div className="home">  
      <h1>Hello There</h1>  
      <p>Welcome my awesome blog</p>  
      <div>  
        <div  
          style={{  
            maxWidth: `300px`,  
            margin: "0 auto 1.45rem"  
          }}  
        >  
          <Image />  
        </div>  
      </div>  
      <Link to="/blogposts/">View all posts</Link>  
    </div>  
  </Layout>  
);export default IndexPage;

Next, find  `page-2.js`  and change the filename to  `blogposts.js`. Gatsby uses the name of any file in the  `pages`  folder as a route name and will make the exported React component available on said route. This means we now have a  `/blogposts`  route. We'll come back to this file later but in the meantime, let's also change a few values in the  `gatsby-config.js`  file. This file sits in the project  `root`.

siteMetadata: {  
    title: `My Awesome Blog`,  
    description: `An awesome blog displaying my awesome posts.`,  
    author: `YOUR_NAME`,  
},

Great! We now have our basic site set up. So we’ll go to the  [Contentful](https://www.contentful.com/)  website and create a new account. It’s pretty painless and you should be set up in no time. By default, they provide an example space but let’s create a fresh one for the project.

Open up the sidebar and click on  **Create Space**. Choose the free option and give your space any name. I’ll call mine  **gatsby-blog**. Select the empty space option, click  **Proceed to confirmation,**  and confirm your options.

After confirming, on the dashboard, click either the “Create Content Type” button or the “Content Model” button in the header and fill in the form that appears. Let’s call the content type  **Blog Post**  and leave the API Identifier as is. Enter any description you’d like.

![](https://miro.medium.com/max/28/1*9tNdtBPtBqcsG5rpyHKYbw.png?q=20)

![](https://miro.medium.com/max/601/1*9tNdtBPtBqcsG5rpyHKYbw.png)

After creating the content type, we’ll start to add some fields to it A field is a building block for our content. If you have a blog post for instance, a few fields could be the  _title_, the  _body_, the  _tags_  and an  _image_. This will generate a form that you’ll fill later on when we start to create actual blog posts. Follow the next steps to create a  _title_  field.

-   Click on the  **Add Field**  button to the right of the dashboard.
-   Select  **Text**  as the type of field you want.

![](https://miro.medium.com/max/30/1*fU0B6MH0_eA05Rx_8dNYJw.png?q=20)

![](https://miro.medium.com/max/684/1*fU0B6MH0_eA05Rx_8dNYJw.png)

-   In the form on the next screen, enter  **title**  as the name, then click on create.
-   Add another text field called  **body**, but after selecting  **Text**, select  **Long ext**  from the radio button on the screen below.

![](https://miro.medium.com/max/30/1*qP8DGKHvp7iF_ChmANiJcg.png?q=20)

![](https://miro.medium.com/max/809/1*qP8DGKHvp7iF_ChmANiJcg.png)

-   Add another field. Select Media as the type instead of Text and call it image.
-   Add a  _tags_  field by selecting Text as the type. Give it tags as a name, and then select the list option on the screen below since we will be storing a list of  _tags_  in this field.

![](https://miro.medium.com/max/30/1*N0wpzih4KYqg0E0pC32VPA.png?q=20)

![](https://miro.medium.com/max/821/1*N0wpzih4KYqg0E0pC32VPA.png)

-   Lastly, create a  _slug_  field. Start by selecting Text as the type and call it slug. This time, instead of clicking Create as above, click on Create and Configure. On the next screen go to the Appearance tab and select slug as the way the field should be displayed. Also, in the Validations tab select unique field to be sure that no two blog posts have the same slugs

![](https://miro.medium.com/max/30/1*fWOc-abYP2qkdEFBx9tuXA.png?q=20)

![](https://miro.medium.com/max/881/1*fWOc-abYP2qkdEFBx9tuXA.png)

Your content model should now look like this:

![](https://miro.medium.com/max/30/1*3wep8DqyueFPu1ThhUFOJg.png?q=20)

![](https://miro.medium.com/max/1726/1*3wep8DqyueFPu1ThhUFOJg.png)

A content model is like a schema that our actual content will follow. You can create all types of models such as case studies, blog posts, product data, page content and so on.

Save your changes and click on the  **Content**  button at the top of the page and select  **Add Blog Post**. I’m going to add three posts with placeholder data, feel free to add as many as you’d like. For images, you can grab some free, open license ones from  [unsplash.com](https://unsplash.com/). Notice how the  `slug`  field gets auto-generated as you enter the title? This will come in handy later.

Awesome! That was a lot but we’re halfway there…

At this point we have our first couple of blog posts and it’s time to bring them into our Gatsby site. For this, we’ll depend on Gatsby’s awesome GraphQL API for pulling in the data. Let’s work on that next.

Go to your settings in Contentful and click on the  **API Keys**  option in the dropdown menu. Create a new API Key and keep the details close by.

Back in your terminal, install the Gatsby plugin we need to start pulling in our Contentful data.

$ yarn add gatsby-source-contentful

We’ll be using Contentful’s  _Content Delivery API_  since we want to retrieve published data only, so be sure to grab the  _Content Delivery API_  key and not the  _Content Preview API key_.

In your  `gatsby-config.js`  file, add the configuration object to the  `plugins`  array:

plugins: [  
    ...  
    {  
      resolve: `gatsby-source-contentful`,  
      options: {  
        spaceId: `YOUR_SPACE_ID`,  
        accessToken: `YOUR_CONTENT_DELIVERY_API_KEY`  
      }  
    }  
],

You should restart your development server again at this point for the new configs to kick in. When the server restarts,  `gatsby-source-contentful`'s GraphQL queries will be available to use.

We can easily test if everything is working by using the GraphiQL playground that Gatsby provides for us. Open  [http://localhost:8000/___graphql](http://localhost:8000/___graphql)  in your browser and run the query below by pasting it into the left window on the page. The query name is  `allContentfulBlogPost`  because our content model is called  **Blog Pos**t. If we had called it  **Product**  or  **Case Study**, then the query made available to us would have been  `allContentfulProduct`  or  `allContentfulCaseStudy`.

{  
  allContentfulBlogPost {  
    edges {  
      node {  
        id  
	slug  
        title  
	tags  
        image {  
          file {  
            url  
          }           
        }  
      }  
    }  
  }  
}

The  `gatsby-source-contentful`  plugin handles all the behind the scenes fetching from the Contentful API using the keys we provided in the  `gatsby-config`  file. It then makes a semantically named GraphQL query available to us.

If it all works, you should see the content you added in the results window to the right of the GraphiQL window in JSON format.

Now that we have connected our Gatsby blog with our Contentful data, we can start building the pages for the blog. Gatsby provides us with a file called  `gatsby-node.js`. This file can be used to dynamically add pages to your site. When Gatsby runs, it will look at the code here and create any pages you tell it to. In the  `gatsby-node.js`  file, let's place the following code:

const path = require(`path`);  
const slash = require(`slash`);exports.createPages = ({ graphql, actions }) => {  
  const { createPage } = actions;  
  // we use the provided allContentfulBlogPost query to fetch the data from Contentful  
  return graphql(  
    `  
      {  
        allContentfulBlogPost {  
          edges {  
            node {  
              id  
              slug  
            }  
          }  
        }  
      }  
    `  
  ).then(result => {  
      if (result.errors) {  
        console.log("Error retrieving contentful data",      result.errors);  
      } // Resolve the paths to our template  
      const blogPostTemplate = path.resolve("./src/templates/blogpost.js"); // Then for each result we create a page.  
      result.data.allContentfulBlogPost.edges.forEach(edge => {  
        createPage({  
          path: `/blogpost/${edge.node.slug}/`,  
          component: slash(blogPostTemplate),  
          context: {  
	    slug: edge.node.slug,  
            id: edge.node.id  
          }  
        });  
      });  
    })  
    .catch(error => {  
      console.log("Error retrieving contentful data", error);  
    });  
};

This module exports a function called  `createPages`. This function has two parameters, graphql, and an actions object. We extract the  `createPage`  action then call the same Graphql query we ran in the GraphiQL playground earlier. We take this result and for each result (each blog post) we call the  `createPage`  function. This function accepts a config object which Gatsby reads when rendering the page. We set the path equal to the concatenated string  `"/blogpost"`  plus the  `slug`. Notice that we also reference a template file at  `./src/templates/blogpost.js`, not to worry, we'll create that file soon.

At this point, kill your server and start it up again. If you enter a dud route like  `[http://localhost:8000/some-non-existent-route/](http://localhost:8000/dskl;sfd/)`  you'll see Gatsby's development 404 page. This page has a list of all the routes and as you can see the newly created pages have been set up.

![](https://miro.medium.com/max/30/1*MDsb5QfV9Zix8NIXSjgpsw.png?q=20)

![](https://miro.medium.com/max/1440/1*MDsb5QfV9Zix8NIXSjgpsw.png)

See why we chose to have a unique slug field? Each post has to have a unique route and using slugs looks so much nicer than using nonsensical ID strings in the URL. Also since Gatsby generates a static site which can have a sitemap, it’s much better for SEO to have your route names match the kind of content you want to rank for.

Now we can concentrate on building out the actual pages.

Create a  `templates`  folder inside your  `src`  folder and add a file called  `blogpost.js`. This will be our template component which will be used every time Gatsby calls the  `createPage`  function in the  `gatsby-node.js`  file.

**NOTE**: Be sure to restart your server at this point if you get any errors. We’re doing a lot of config stuff and Gatsby may need a restart in order to run everything properly.

import React from "react";  
import { Link, graphql } from "gatsby";  
import Layout from "../components/layout";  
import SEO from "../components/seo";const BlogPost = ({ data }) => {  
  const { title, body, image, tags } = data.contentfulBlogPost;  
  return (  
    <Layout>  
      <SEO title={title} />  
      <div className="blogpost">  
        <h1>{title}</h1>  
        <img alt={title} src={image.file.url} />  
        <div className="tags">  
          {tags.map(tag => (  
            <span className="tag" key={tag}>  
              {tag}  
            </span>  
          ))}  
        </div>  
        <p className="body-text">{body.body}</p>  
        <Link to="/blogposts">View more posts</Link>  
        <Link to="/">Back to Home</Link>  
      </div>  
    </Layout>  
  );  
};export default BlogPost;export const pageQuery = graphql`  
  query($slug: String!) {  
    contentfulBlogPost(slug: { eq: $slug }) {  
      title  
      slug  
      body {  
        body  
      }  
      image {  
        file {  
          url  
        }  
      }  
      tags  
    }  
  }  
`;

At the bottom of the page, we export a Graphql query. Gatsby will run this query at runtime and will pass a  **data**  prop to  **BlogPost**  containing the Contentful data. Note that in this case we are querying a single post and passing the slug along as a filter parameter. We’re basically asking for the post which matches the passed in slug (`contentfulBlogPost(slug: { eq: $slug })`). This slug is made available to us because we passed it in as a page context in our  `gatsby-config.js`.

The rest is straightforward React. We create a component and using the  **data**  prop, we populate the page content. We have no styling yet but we’ll get to that in a bit.

What we need now is a page to list all the available blog post pages. We cannot rely on going to the 404 page every time we need to read a blog post!

Let’s head back to the  `blogposts.js`  file in the  `pages`  folder that we created at the beginning of this project and tweak it.

import React from "react";  
import { Link, graphql } from "gatsby";import Layout from "../components/layout";  
import SEO from "../components/seo";const BlogPosts = ({ data }) => {  
  const blogPosts = data.allContentfulBlogPost.edges;  
  return (  
    <Layout>  
      <SEO title="Blog posts" />  
      <h1>{"Here's a list of all blogposts!"}</h1>  
      <div className="blogposts">  
        {blogPosts.map(({ node: post }) => (  
          <div key={post.id}>  
            <Link to={`/blogpost/${post.slug}`}>{post.title}</Link>  
          </div>  
        ))}  
        <span className="mgBtm__24" />  
        <Link to="/">Go back to the homepage</Link>  
      </div>  
    </Layout>  
  );  
};export default BlogPosts;export const query = graphql`  
  query BlogPostsPageQuery {  
    allContentfulBlogPost(limit: 1000) {  
      edges {  
        node {  
          id  
          title  
          slug  
          body {  
            body  
          }  
          image {  
            file {  
              url  
            }  
          }  
          tags  
        }  
      }  
    }  
  }  
`;

The pattern should be familiar now.

At the bottom of the page, we export a GraphQL query. The query is the same as the one we used in  `gatsby-node.js`  to generate the blogpost pages. It pulls all the Contentful data of the  **BlogPost**  type. Gatsby makes the result of the query available to us in the data object just as with the individual blogpost page. For this page though, we only need the  `id`,  `title`,  `slug`  and  `tags`  fields.

At this point, let’s add some very basic styling. For the sake of this example, we’ll just add a few lines to the end of the  `layout.css`  file, but in a real-world project you'd probably not want to do this. Go with whatever method you are comfortable with.

/* Add these lines to the end of the layout.css file */  
@import url("<https://fonts.googleapis.com/css?family=Open+Sans:300,400,600>");  
html {  
  font-family: "Open Sans";  
}header {  
  /* We use !important here to override  
  the inline styles just for this example.  
  in production code, avoid using it where  
  possible*/  
  background-color: cadetblue !important;  
}header div {  
  text-align: center;  
}header div h1 {  
  font-weight: 600;  
}.home {  
  text-align: center;  
}.home img {  
  margin: auto;  
}.blogpost {  
  font-size: 18px;  
  width: 35em;  
}h1 {  
  font-weight: 400;  
  margin-top: 48px;  
  font-family: "Open Sans";  
}img {  
  margin-bottom: 8px;  
}.tags {  
  margin-bottom: 24px;  
}.tags span.tag {  
  font-weight: bold;  
  margin-right: 8px;  
  background: cadetblue;  
  padding: 2px 12px;  
  border-radius: 4px;  
  color: white;  
  font-size: 12px;  
}.blogpost p.body-text {  
  margin-bottom: 32px;  
}p {  
  line-height: 1.8;  
  color: #929191;  
  font-weight: 300;  
}.blogpost a {  
  display: block;  
  margin-bottom: 8px;  
}.blogposts a {  
  display: block;  
  margin-bottom: 8px;  
}footer {  
  margin-top: 120px;  
}.mgBtm__24 {  
  display: inline-block;  
  margin-bottom: 24px;  
}

Now we have our blog, the next step is to deploy it and make it available for all the world to see. With Netlify this is super easy. Netlify integrates really well with GitHub. In your terminal, run:

$ git init

Go to your GitHub and create a new repo called  `gatsby-contentful-blog-starter`, then follow the commands for pushing to an existing repository.

$ git add .  
$ git commit -m 'initial commit'  
$ git remote add origin git@github.com:YOUR_GITUHB_USERNAME/gatsby-contentful-blog-starter.git  
$ git push -u origin master

With your code pushed to GitHub, head over to  [Netlify](https://www.netlify.com/)  and create an account. In your dashboard click on’**New site from Git**, select  **GitHub**  as a provider and go through the authorization process selecting whatever options you feel comfortable with.

Next, select a repo from the list provided. if you can’t find the repo we just created, select  **Configure the Netlify app on GitHub**. This will open a popup allowing you to choose the repo you want to authorize for use with Netlify. Follow the prompts till you find the repo. After selecting our blog project, you’ll be redirected to the Netlify deploy screen and you should now be able to select the  `gatsby-contentful-blog-starter`  repo. As you can see, Netlify knows how to build Gatsby sites so you can just click the  **Deploy Site**  button at the end of the page.

![](https://miro.medium.com/max/30/1*dCCihyxDW2u7YHqqYnpUzQ.png?q=20)

![](https://miro.medium.com/max/1158/1*dCCihyxDW2u7YHqqYnpUzQ.png)

Netlify runs Gatsby sites really easy with minimal configuration. Your new site should be ready in a few minutes.

![](https://miro.medium.com/max/30/1*RZgyGNpt1_gAunFTpCF4eQ.png?q=20)

![](https://miro.medium.com/max/1224/1*RZgyGNpt1_gAunFTpCF4eQ.png)

Remember how we had to kill the server and restart it to fetch new data? Well, we don’t want to have to trigger a redeploy manually every time someone adds or changes content in Contenful. The solution to that is to use Contentful’s hooks to trigger an automatic Netlify redeploy of our site (Yup, this triple tag-team thought of everything).

This means that new pages will get added to your blog automatically for each new blog post you add. Also, if you’re using the Gatsby sitemap plugin, the new pages will be included in the sitemap when it gets regenerated on deployment, making it much easier to rank for keywords and help your SEO efforts with minimal fuss.

On Netify click on  **Site Settings**  and then in the left menu, select  **Build & Deploy**. Look for the  **Add build hook**  button and click on it, giving the build hook a name (I am using “**contentful**”) and then click on  **Save**.

Now copy the  **buildhook**  url and go back to your Contentful dashboard. Hit the settings dropwdown and select  **Webhooks**. The Webhooks screen already has a template for Netlify in the bottom right. Click on this.

![](https://miro.medium.com/max/30/1*XoT3vHclyt7RjAGyp9eJQQ.png?q=20)

![](https://miro.medium.com/max/1219/1*XoT3vHclyt7RjAGyp9eJQQ.png)

In the form that appears, add the Netlify build hook url and click  **Create Webhook**.

Now go back to the  **Content**  page and add a new blog post. As soon as you hit publish, Contentful will make an API call to the build hook you provided. This will in turn, cause Netlify to redeploy your site. Gatsby will pull in the Contentful data all over again, which now includes the new post you added, and create a new page based on the new blog post.

And that’s it! It’s been quite a journey, but now we have a working blog using three awesome tools that work so well together. From here you can add more content types and pages, expand the site or start a new project from scratch. Happy hacking!

[**Source :**](https://itnext.io/content-management-with-gatsby-netlify-and-contentful-70f03de41602)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyOTE2NzIxNTddfQ==
-->