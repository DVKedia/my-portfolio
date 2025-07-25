# Next.js and Tailwind Résumé

A résumé built especially with software professionals in mind. Impress your potential employer with a beautiful and incredibly fast résumé website, or generate a PDF for email and print.

[See an example](https://my-portfolio-alpha-murex-79.vercel.app/)

Your résumé can also generate a secure URL that will display information not accessible on the public URL. The secure version can include private information such as email, phone number, and mailing address. You can send the private link to a potential employer or use it to generate a more complete PDF for yourself.

## Features

- Update your résumé with simple Markdown files
  - Type safe content management using [Contentlayer](https://www.contentlayer.dev/)
  - Integration with external CMS systems will be possible in the future
- Beautiful and accessible web app to view your résumé, link on social media, and send to potential employers
- Use a secret link to generate the résumé with additional private information
- Generate a PDF on demand to view, download, or print in light or dark mode
- Easily customizable
  - 19 accent color palettes out-of-the-box
  - 6 neutral color palettes out-of-the-box
  - Automatic light and dark modes for each palette
  - Tailwind classes to modify app and generated images
- Dynamic OG share images in light or dark mode

## Technology

- [Next.js](https://nextjs.org)
- [TypeScript](https://www.typescriptlang.org/)
- [Tailwind CSS v4](https://tailwindcss.com/)
- [Contentlayer](https://www.contentlayer.dev/)
- [React-pdf](https://react-pdf.org/)
- [Strum Colors](https://www.strum.design/colors)
- [Testing Library](https://testing-library.com/)

## How To Use This Project

The project requires only a few steps to set up your custom config, add content to the internal CMS, and deploy to Vercel or Netlify!

### Clone and Deploy

The simplest way to get started is to clone and deploy in one step. Afterwards, you can edit the CMS and template to match your needs.

The project is designed to be deployed on [Netlify](https://netlify.com) or [Vercel](https://vercel.com). You can click one of the following buttons to clone the repo, set environment variables, and deploy.

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/colinhemphill/nextjs-resume)

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https%3A%2F%2Fgithub.com%2Fcolinhemphill%2Fnextjs-resume&env=PRIVATE_KEY&envDescription=Environment%20variables%20needed%20to%20run%20the%20application%20and%20provide%20private%20information%20links&envLink=https%3A%2F%2Fgithub.com%2Fcolinhemphill%2Fnextjs-resume%23environment-variables&project-name=nextjs-resume&repo-name=nextjs-resume&demo-title=Next.js%20R%C3%A9sum%C3%A9&demo-description=An%20example%20Next.js%20static%20r%C3%A9sum%C3%A9)

### Development

To customize your résumé, clone the project you just created to your local machine and `cd` to it.

```bash
cd my-resume
npm i
```

I've tested the project with `bun`, `npm`, `pnpm`, and `yarn` and haven't run into any notable issues. For development the test runner defaults to `bun`.

### Modify Custom Config

Open the project in your favorite editor, and go to the `edit-me/config/` folder at the root where you can edit the `resume-config.ts` file to meet your needs. The config file contains the following constants that will be used throughout the project (these are typed to provide appropriate autocomplete and error checking):

- `accentColor`: `AccentColor`. The name of an accent palette from [Strum Colors](https://www.strum.design/colors/documentation/colors#accents). If using a standard color, the contrasting text color will be white, and if using a bright color, the contrasting text color will be black.
- `neutralColor`: `NeutralColor`. The name of a neutral palette from [Strum Colors](https://www.strum.design/colors/documentation/colors#neutrals).
- `appTheme`: `'system' | 'light' | 'dark'`. If `appTheme` is set to `system`, the résumé site will default to the user's system preference. If set to `light` or `dark` the user's preference will be overriden.
- `imageTheme`: `'light' | 'dark'`. Your OG share image and app icons will be generated in either a light or a dark variant.
- `pdfTheme`: `'light' | 'dark'`. Your PDF will be generated in either a light or a dark variant.

You'll also find `links.ts` which generates external links at the bottom of the document. You can use any icon from [Simple Icons](https://simpleicons.org/) alongside these links.

### Set Up Your CMS

Next, modify the mock CMS data that is included in `edit-me/content/`. Each Markdown file uses Front Matter fields that are used to add attributes to the item. These attributes are type safe, so the project won't run if required fields are missing or invalid. The rest of the Markdown file will be rendered as HTML to provide a description of the item.

Although the mock files should be pretty self-explanatory, you can view the [Contentlayer config](contentlayer.config.ts) for detailed descriptions of required and optional fields.

### Environment Variables

Regardless of where the app is deployed, it may need access to the following environment variables:

- `PRIVATE_KEY` (optional): this is a code, determined by the author, which will provide URL access to a version of the résumé that includes private information. We recommend generating this code (e.g. a UUID or using a password generator).

## Private Link

Your project can be configured to provide a secret URL that will display more information than the public URL. This is helpful if you want to send a complete résumé to a potential employer, or if you want to generate a PDF for your own use. In this version, you can include personal information such as email, phone number, and address that you don't want visible to the general public.

### Setup

The private URL will only work if you added a `PRIVATE_KEY` environment variable. If working locally, you can add this in a `.env.local` file:

```
PRIVATE_KEY=your-private-key
```

You can then visit `https://your-url.com/private/your-private-key` to see the private version of the résumé.

### Adding Private Content

For the built-in Markdown integration, please note that you **must be sure to not commit the private information to a public Git repo**. Only use this feature in a private repo, and even then _please be aware_ of the security concerns around commiting private information to any Git repo.

To add private data to the CMS, simply add it to the `privateFields` folder.

- `cms/privateFields/`. Add as many private contact information fields as you want to display. They will appear in the order they are arranged in the folder, so you can use a number prefix to order them.
  - `label`: **required string**. The label of the field, such as "Email" or "Address".

### Security

This private URL is _only as secure as the people you send it to_. To invalidate an old private URL, you simply need to change the `PRIVATE_KEY` environment variable.

## Design and Customizations

The template is built to be responsive, beautiful, and accessible right out of the box. It supports automatic dark/light mode themeing in the web version, and a great single-page print layout in the PDF version. The project supports a minimal set of configurations such as accent colors, but if you're a front end developer or designer, you can easily open up the source code and customize it however you see fit.

If you really want to go deep on customization, you have full control of the Tailwind configuration in the [styles](/src/app/styles) folder.

We use [ImageResponse API](https://nextjs.org/docs/app/api-reference/file-conventions/metadata/opengraph-image) to generate dynamic Open Graph share images and app icons. You can edit the layout, styles, and text of OG Image using Tailwind classes in `src/app/opengraph-image.tsx` and the icon in `src/app/icon.tsx`.

This dynamic share image will use your custom color settings, as well as data from the CMS.

## Getting the Latest Updates

To sync your personal résumé with the newest version of this project, you can do the following:

```bash
// add the original repo as a git remote
git remote add upstream git@github.com:colinhemphill/nextjs-resume.git

// pull changes from upstream
git pull upstream main
```

Then resolve any merge conflicts and make your desired changes. You'll need to look over the [CHANGELOG](/CHANGELOG.md) to see what happened since the last time you pulled, and please note that upstream changes could break your customizations!
