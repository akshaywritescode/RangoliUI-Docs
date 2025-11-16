---
sidebar_position: 3
---

# Separator
Separator Component Helps you to separate content in components or making a divider.
![Separator Image](/img/separator.png)<br />
[View Live Example Here](https://rangoli-ui-live-components.vercel.app/separator)

## Does this depend on any other rangoli components?
No, Separator is an independent component, it’s not depend on any other rangoli components.

## Usage
```tsx
<Separator className="w-full" />
```

## Component Code
```tsx
"use client";

import { useTheme } from "next-themes";
import { useEffect, useState } from "react";

type TSeparator = {
  className?: string;
};

export default function Separator({ className }: TSeparator) {
  const { theme } = useTheme();
  const [mounted, setMounted] = useState(false);

  useEffect(() => {
    setMounted(true);
  }, []);

  // Avoid rendering theme-based class until mounted
  const themeClass = !mounted ? "" : theme === "light" ? "bg-black/10" : "bg-white/10";

  return <div className={`${className} ${themeClass} h-[1px]`} />;
}
```
