---
sidebar_position: 2
---

# Theme Switcher
A customizable theme switcher component that enables seamless toggling between light and dark modes, To use the theme switcher, ensure you have dark mode functionality set up in your project. Follow the official dark mode [setup guide](/docs/Getting%20Started/Theme) for proper configuration.

![Theme Switcher](/img/theme-switcher.png)<br />
[View Live Example Here](https://rangoli-ui-live-components.vercel.app/theme-switcher)

## Does this depend on any other rangoli components?
No, Language Switcher is an independent component, it’s not depend on any other rangoli components.

## Usage
```tsx
<ThemeSwitcher defaultValue="dark" />
```

## Component Code
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
