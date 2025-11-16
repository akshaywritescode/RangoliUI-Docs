---
sidebar_position: 4
---

# Dark & Light Theme

You need to have ShadCN Installed, to toggle between light and dark theme, visit [Shadcn Installation Documentation](https://ui.shadcn.com/docs/installation).

## Install Next Theme
```json
npm install next-themes
```

## Create a theme provider
Create `@/app/providers/ThemeProvider.tsx` a theme provider to access theme switching for all rangoli components.

```tsx
"use client"

import * as React from "react"
import { ThemeProvider as NextThemesProvider } from "next-themes"

export function ThemeProvider({
  children,
  ...props
}: React.ComponentProps<typeof NextThemesProvider>) {
  return <NextThemesProvider {...props}>{children}</NextThemesProvider>
}
```

## Wrap your root layout with `ThemeProvider.tsx`
```tsx
import { ThemeProvider } from "@/app/providers/ThemeProvider";

export default function RootLayout({ children }: RootLayoutProps) {
  return (
    <>
      <html lang="en" suppressHydrationWarning>
        <head />
        <body>
          <ThemeProvider
            attribute="class"
            defaultTheme="system"
            enableSystem
            disableTransitionOnChange
          >
            {children}
          </ThemeProvider>
        </body>
      </html>
    </>
  )
}
```

## Creating a `ThemeSwitcher.tsx` component to toggle between dark & light mode.
Create `@/app/components/ThemeSwitcher.tsx` to toggle between themes
```tsx
//Run The following command to install required shadcn component
//npx shadcn@latest add tabs

"use client"

import { Tabs, TabsList, TabsTrigger } from "@/components/ui/tabs"; 
import { Laptop, MoonIcon, SunIcon } from "lucide-react";
import { useTheme } from "next-themes"

type TThemeSwicther = {
    defaultValue: "system" | "light" | "dark",
    className?: "string"
}

export default function ThemeSwitcher({ defaultValue }: TThemeSwicther) {
    const { setTheme } = useTheme();

    return (
        <Tabs defaultValue={defaultValue}>
            <TabsList>
                <TabsTrigger value="system" onClick={() => setTheme("system")}>
                    <Laptop className="w-4" />
                </TabsTrigger>
                <TabsTrigger value="dark" onClick={() => setTheme("dark")}>
                    <MoonIcon className="w-4" />
                </TabsTrigger>
                <TabsTrigger value="light" onClick={() => setTheme("light")}>
                    <SunIcon className="w-4" />
                </TabsTrigger>
            </TabsList>
        </Tabs>
    );
}
```

## Using Theme Switcher Component
Import `ThemeSwitcher` component wherever you want to put your theme toggle component.
![Theme Toggle](/img/theme-switcher.avif)

```tsx
"use client";

import { LanguageSwitcher } from "./components/LanguageSwitcher";
import TestimonialCard from "./components/TestimonialCard";
import ThemeSwitcher from "./components/ThemeSwitcher";
import testimonialAvatar1 from "./favicon.ico";
import { useI18n } from "@/app/providers/i18nProvider";

export default function Home() {
  const { t } = useI18n();

  return (
    <div className="w-screen h-screen flex justify-center items-center">
      <ThemeSwitcher defaultValue="dark" /> //imported & used here
      <LanguageSwitcher />
      <TestimonialCard
        description={t("testimonial_description")}
        testimonialAvatar={testimonialAvatar1}
        testimonialAvatarAlt="Avatar 1"
        testimonialName="Jammie Riveria"
        testimonialUserHandle="@jammietech123"
      />
    </div>
  );
}
```