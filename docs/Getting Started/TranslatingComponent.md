---
sidebar_position: 3
---

# Translating Rangoli Components

To translate rangoli component we have to put the `key:value` pair of component text that we want to translate.

## Translating Testimonial Component
![Testimonial Card Image](/img/testimonial-card.avif)

## Putting text content of it's test on `/i18n/en.json` file
```json
{
  "testimonial_description": "Rangoli UI is a game-changer! The prebuilt components saved me hours of development time while maintaining top-notch design quality.",
}
```

## Running the translation job (generate target JSONs)
```json
npx lingo.dev@latest run
```

This command will create target files with their respective translations. For example, `i18n/hi.json` will contain the Hindi translation, like this:
```json
{
  "greeting": "आपके कंपोनेंट का यह टेक्स्ट Lingo.dev द्वारा अनुवादित किया जाएगा"
}
```

## Add a small client i18n provider that uses these JSON files
Create `/app/providers/i18nProvider.tsx` (client component). This is the provider it's supply translated target to the components.

```tsx
"use client";

import React, { createContext, useContext, useMemo, useState } from "react";
import en from "@/i18n/en.json";
import hi from "@/i18n/hi.json";
import de from "@/i18n/de.json";
import zh from "@/i18n/zh.json";
import ja from "@/i18n/ja.json";
import ko from "@/i18n/ko.json";
import es from "@/i18n/es.json";

type LocaleKey = "en" | "hi" | "de" | "zh" | "ja" | "ko" | "es";

const messagesMap: Record<LocaleKey, Record<string, string>> = {
  en, hi, de, zh, ja, ko, es
};

const I18nContext = createContext<{
  locale: LocaleKey;
  setLocale: (l: LocaleKey) => void;
  t: (key: string) => string;
} | null>(null);

export function I18nProvider({ children }: { children: React.ReactNode }) {
  const [locale, setLocale] = useState<LocaleKey>("en");

  const t = useMemo(() => {
    return (key: string) => {
      const val = messagesMap[locale]?.[key];
      if (typeof val === "string") return val;
      // fallback: try english, else return key
      return messagesMap["en"][key] ?? key;
    };
  }, [locale]);

  return (
    <I18nContext.Provider value={{ locale, setLocale, t }}>
      {children}
    </I18nContext.Provider>
  );
}

export function useI18n() {
  const ctx = useContext(I18nContext);
  if (!ctx) throw new Error("useI18n must be used inside I18nProvider");
  return ctx;
}

```

## Wrap your app with the provider
Edit `/app/layout.tsx` (root layout). Wrap children with I18nProvider

```tsx
import "./globals.css";
import { I18nProvider } from "@/app/providers/i18nProvider";

export default function RootLayout({ children, params }: { children: React.ReactNode; params?: any }) {
  return (
    <html lang="en">
      <body>
        <I18nProvider>{children}</I18nProvider>
      </body>
    </html>
  );
}
```

## Add Language Switcher component to switch between different languages in UI.
Add a new component `app/components/LanguageSwitcher.tsx`. This component will allow users to switch the UI between different languages.

```tsx
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
          {languages.find(l => l.value === locale)?.label ?? "select_language"}
          <ChevronsUpDown className="opacity-50" />
        </Button>
      </PopoverTrigger>
      <PopoverContent className="w-[200px] p-0">
        <Command>
          <CommandInput placeholder={"select_language"} className="h-9" />
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

## Update Testimonial Card to support translation
![Live Demo](/img/live-demo.png)
```tsx
"use client";

import { LanguageSwitcher } from "./components/LanguageSwitcher";
import TestimonialCard from "./components/TestimonialCard";
import testimonialAvatar1 from "./favicon.ico";
import { useI18n } from "@/app/providers/i18nProvider";

export default function Home() {
  const { t } = useI18n();

  return (
    <div className="w-screen h-screen flex justify-center items-center">
      <LanguageSwitcher /> //Put whereever you want to put language switcher component
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
