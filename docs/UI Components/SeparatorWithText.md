---
sidebar_position: 4
---

# Separator with text
Separator with text component helps you to separate content in components with text included on sepration.<br />
![Separator Image](/img/separator-with-text.png)<br />
[View Live Example Here](https://rangoli-ui-live-components.vercel.app/separator-with-text)

## Does this depend on any other rangoli components?
No, Separator with text is an independent component, it’s not depend on any other rangoli components.

## Usage
```tsx
<SeparatorWithText text="or login with" className="w-full" />
```

## Component Code
```tsx
"use client";

import { useTheme } from "next-themes";
import { useEffect, useState } from "react";

type TSeparator = {
    className?: string;
    text: string;
};

export default function SeparatorWithText({ className, text }: TSeparator) {
    const { theme } = useTheme();
    const [mounted, setMounted] = useState(false);

    useEffect(() => {
        setMounted(true);
    }, []);

    // Avoid rendering theme-based class until mounted
    const separatorBgColor = !mounted ? "" : theme === "light" ? "bg-black/10" : "bg-white/10";


    return <div className={`${className} ${separatorBgColor} h-[1px] relative`}>
        <span className={`px-2 text-sm text-muted-foreground absolute left-1/2 -translate-x-1/2 bottom-1/2 translate-y-1/2 bg-card`}>{text}</span>
    </div>;
}
```
