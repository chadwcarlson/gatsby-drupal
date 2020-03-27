# Gatsby Drupal multi-app for Platform.sh

<p align="center">
<a href="https://console.platform.sh/projects/create-project?template=https://raw.githubusercontent.com/platformsh/template-builder/master/templates/gatsby-drupal/.platform.template.yaml&utm_content=gatsby-drupal&utm_source=github&utm_medium=button&utm_campaign=deploy_on_platform">
    <img src="https://platform.sh/images/deploy/lg-blue.svg" alt="Deploy on Platform.sh" width="180px" />
</a>
</p>

This template builds a multi-app project using Gatsby as its frontend and a Drupal backend to store content using Gatsby's Drupal source plugin.

Gatsby is a free and open source framework based on React that helps developers build blazing fast websites and apps, and WordPress is a blogging and lightweight CMS written in PHP.

## Services

* Node.js 12
* PHP 7.3
* MariaDB 10.4

## Post-install

1. When you initially deploy the template, you will receive a `403` error on the base route. There is not yet any content to build the Gatsby site, because Wordpress has not yet been fully installed. Visit the `backend.<generated url>` subdomain, and run through the Wordpress installer as normal. You will not be asked for database credentials as those are already provided.
2. Once you have completed the Wordpress install, redeploy the environment with `platform redeploy -p <PROJECT ID> -e master`.

## Customizations

The following files and additions make the framework work.  If using this project as a reference for your own existing project, replicate the changes below to your project.

* The `.platform.app.yaml`, `.platform/services.yaml`, and `.platform/routes.yaml` files have been added.  These provide Platform.sh-specific configuration and are present in all projects on Platform.sh.  You may customize them as you see fit.
* Additional Platform.sh configuration reader modules for both [PHP](https://github.com/platformsh/config-reader-php) and [Node.js](https://github.com/platformsh/config-reader-nodejs) have been added. They provide convenience wrappers for accessing the Platform.sh environment variables.
* `gatsby-config.js` has been modified to read the Wordpress backend url and assign it to the `baseUrl` attribute for the `gatsby-source-wordpress` plugin. Since routes are not available during the build hook, and since we want this value to be generated and unique on each environment, `gatsby build` runs and pulls in content from the Wordpress app during the `post_deploy` hook on the mounted `public` directory. `gatbsby-source-wordpress` can have additional parameters set to modify your configuration, so consult the [documentation](https://www.gatsbyjs.org/packages/gatsby-source-wordpress/#how-to-use).

## References

- [`gatsby-source-drupal`](https://www.gatsbyjs.org/packages/gatsby-source-drupal/)
- [Using Gatsby with Drupal](https://www.gatsbyjs.com/guides/drupal/)
- [Sourcing from Drupal](https://www.gatsbyjs.org/docs/sourcing-from-drupal/)
- [Using Drupal with Gatsby on GitHub](https://github.com/gatsbyjs/gatsby/tree/master/examples/using-drupal)
- [PHP on Platform.sh](https://docs.platform.sh/languages/php.html)
- [Node.js on Platform.sh](https://docs.platform.sh/languages/nodejs.html)
