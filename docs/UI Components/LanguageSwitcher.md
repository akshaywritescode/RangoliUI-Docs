---
sidebar_position: 1
---

# Language Switcher
A language switcher component that enables seamless toggling between different languages, To use the language switcher, ensure you have properly setup Lingo.dev with rangoli. Follow the following docs [Setting up lingo.dev](/docs/Getting%20Started/AutoTranslate) and [Translating Rangoli Components](/docs/Getting%20Started/TranslatingComponent).

![Language Selector](/img/language-selector.png)<br />
[View Live Example Here](https://rangoli-ui-live-components.vercel.app/language-switcher)

## Does this depend on any other rangoli components?
No, Theme Switcher is an independent component, it’s not depend on any other rangoli components.

## Usage
```tsx
<LanguageSwitcher  />
```

## Component Code
```tsx
//Run The following command to install required shadcn component
//npx shadcn@latest add command
//npx shadcn@latest add button
//npx shadcn@latest add popover


"use client";

import * as React from "react";
import { Check, ChevronsUpDown } from "lucide-react";
import { cn } from "@/lib/utils";
import { Button } from "@/components/ui/button";
import { Command, CommandGroup, CommandItem, CommandList, CommandInput, CommandEmpty } from "@/components/ui/command";
import { Popover, PopoverContent, PopoverTrigger } from "@/components/ui/popover";
import { useI18n } from "@/app/providers/i18nProvider"; 

const languages = [
  { value: "en", label: "English" },
  { value: "hi", label: "हिन्दी" },
  { value: "de", label: "Deutsch" },
  { value: "zh", label: "中文" },
  { value: "ja", label: "日本語" },
  { value: "ko", label: "한국어" },
  { value: "es", label: "Español" }
];

export function LanguageSwitcher() {
  const { locale, setLocale} = useI18n();
  const [open, setOpen] = React.useState(false);

  return (
    <Popover open={open} onOpenChange={setOpen}>
      <PopoverTrigger asChild>
        <Button variant="outline" role="combobox" aria-expanded={open} className="w-[200px] justify-between">
          {languages.find(l => l.value === locale)?.label ?? "Select Language..."}
          <ChevronsUpDown className="opacity-50" />
        </Button>
      </PopoverTrigger>
      <PopoverContent className="w-[200px] p-0">
        <Command>
          <CommandInput placeholder={"Select Language..."} className="h-9" />
          <CommandList>
            <CommandEmpty>No language found.</CommandEmpty>
            <CommandGroup>
              {languages.map((language) => (
                <CommandItem
                  key={language.value}
                  value={language.value}
                  onSelect={() => {
                    setLocale(language.value as any);
                    setOpen(false);
                  }}
                >
                  {language.label}
                  <Check className={cn("ml-auto", locale === language.value ? "opacity-100" : "opacity-0")} />
                </CommandItem>
              ))}
            </CommandGroup>
          </CommandList>
        </Command>
      </PopoverContent>
    </Popover>
  );
}
```
