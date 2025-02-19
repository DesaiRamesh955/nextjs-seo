
This documentation covers all important SEO configurations for **Next.js 14 (App Router)**, including metadata, structured data, Open Graph, Twitter cards, robots.txt, sitemap, and canonical URLs.

----------

## 1️⃣ Metadata Configuration (`generateMetadata` in `page.tsx`)

Next.js provides `generateMetadata()` for setting **title, description, canonical URL, Open Graph, and Twitter metadata**.

### **Example:**

```tsx
import { Metadata } from "next";
import Script from "next/script";

export const generateMetadata = (): Metadata => {
  const title = "Your Page Title | Brand Name";
  const description = "A brief and compelling description of your page.";
  const canonical = "https://www.yourwebsite.com/page-url";
  const imageUrl = "https://www.yourwebsite.com/og-image.jpg";

  return {
    title,
    description,
    authors: [{ name: "Your Brand Name" }],
    alternates: {
      canonical,
    },
    openGraph: {
      title,
      description,
      url: canonical,
      siteName: "Your Site Name",
      images: [{ url: imageUrl, width: 1200, height: 630, alt: "OG Image" }],
      type: "website",
      locale: "en_US",
    },
    twitter: {
      card: "summary_large_image",
      site: "@YourTwitterHandle",
      title,
      description,
      images: [imageUrl],
    },
  };
};

```

✅ **Includes:** Title & description, canonical URL, Open Graph (`og:title`, `og:image`), Twitter Card (`twitter:title`, `twitter:image`).

----------

## **2️⃣ Structured Data (JSON-LD) for Rich Snippets**

Use **Google Schema Markup** (`@type`) to enhance search visibility.

### **Example: JSON-LD for a Web Page (`page.tsx`)**

```tsx
export default function Page() {
  const jsonLd = {
    "@context": "https://schema.org",
    "@type": "WebPage",
    "name": "Your Page Title",
    "description": "A brief and compelling description of your page.",
    "url": "https://www.yourwebsite.com/page-url",
    "author": { "@type": "Organization", "name": "Your Brand Name" },
  };

  return (
    <>
      <Script
        id="json-ld"
        type="application/ld+json"
        dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
      />
      <main>
        <h1>Your Page Content</h1>
      </main>
    </>
  );
}

```

✅ Supports **Google Rich Results**, helps with **SEO & rankings**.

----------

## **3️⃣ robots.txt (for Crawling & Indexing)**

### **Create `robots.txt` in `app/robots.ts`**

```tsx
import { MetadataRoute } from "next";

export default function robots(): MetadataRoute.Robots {
  return {
    rules: [
      {
        userAgent: "*",
        allow: "/",
        disallow: ["/admin", "/private-page"],
      },
    ],
    sitemap: "https://www.yourwebsite.com/sitemap.xml",
  };
}

```

✅ Allows Google to **crawl important pages**, blocks **sensitive/private routes**.

----------

## **4️⃣ Sitemap.xml (for Search Engines)**

A sitemap helps search engines **discover your pages**.

### **Create `sitemap.ts` in `app/sitemap.ts`**

```tsx
import { MetadataRoute } from "next";

export default function sitemap(): MetadataRoute.Sitemap {
  return [
    {
      url: "https://www.yourwebsite.com/",
      lastModified: new Date(),
      priority: 1.0,
      changeFrequency: "daily",
    },
    {
      url: "https://www.yourwebsite.com/page-url",
      lastModified: new Date(),
      priority: 0.8,
      changeFrequency: "weekly",
    },
  ];
}

```

✅ Google **discovers & indexes** pages faster, improves **SEO rankings**.

----------

## **5️⃣ HTML Meta Tags (For SEO & Performance)**

Modify `layout.tsx` (`app/layout.tsx`).

```tsx
export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en">
      <head>
        <link rel="icon" href="/favicon.ico" />
        <link rel="canonical" href="https://www.yourwebsite.com/page-url" />
        <meta name="viewport" content="width=device-width, initial-scale=1" />
        <meta name="google-site-verification" content="YOUR_VERIFICATION_CODE" />
      </head>
      <body>{children}</body>
    </html>
  );
}

```

✅ Includes **favicon, canonical URL, mobile viewport, Google verification**.

----------

## **6️⃣ Dynamic Metadata for Each Page**

If your site has **dynamic pages**, use metadata based on URL params.

### **Example: Dynamic Metadata in `[slug]/page.tsx`**

```tsx
type Props = { params: { slug: string } };

export const generateMetadata = ({ params }: Props): Metadata => {
  const title = `${params.slug.replace("-", " ")} | Your Site`;
  const description = `Read about ${params.slug.replace("-", " ")} on our website.`;

  return {
    title,
    description,
    alternates: { canonical: `https://www.yourwebsite.com/${params.slug}` },
  };
};

```

✅ **Dynamically updates SEO metadata** for each page.

----------

## **7️⃣ Open Graph Preview Debugging**

To **test your metadata & structured data**, use:

-   [Google Rich Results Test](https://search.google.com/test/rich-results)
-   [Facebook Debugger](https://developers.facebook.com/tools/debug/)
-   [Twitter Card Validator](https://cards-dev.twitter.com/validator)

----------

## **🎯 Final Checklist**

✅ **Metadata (Title, Description, Open Graph, Twitter)**  
✅ **Structured Data (JSON-LD for SEO)**  
✅ **robots.txt (Controls crawling)**  
✅ **sitemap.xml (Improves indexing)**  
✅ **Canonical URLs (Avoids duplicate content issues)**  
✅ **HTML Meta Tags (Performance & SEO settings)**  
✅ **Dynamic Metadata (For dynamic pages)**

----------
