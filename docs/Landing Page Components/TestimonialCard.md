---
sidebar_position: 2
---

# Testimonial Card

Testimonial card component helps you to show testimonial in you landing pages<br /><br />
![Testimonial Card](/img/testimonial-card.png)<br />
[View Live Example Here](https://rangoli-ui-live-components.vercel.app/testimonial-card)

## Does this depend on any other rangoli components?

No, Testimonial Card is an independent component, it’s not depend on any other rangoli components.

## Usage

```tsx
<div className="w-full h-full flex justify-center items-center">
  <TestimonialCard
    description={t("testimonial-1")}
    testimonialAvatar={testimonialAvatar1}
    testimonialAvatarAlt="Avatar 1"
    testimonialName="Jammie Riveria"
    testimonialUserHandle="@jammietech123"
  />
</div>
```

## Component Code
```tsx
//Run The following command to install required shadcn component
//npx shadcn@latest add card


import { Card, CardContent, CardFooter } from "@/components/ui/card";
import Image, { StaticImageData } from "next/image";

type TTestimonialCard = {
    description: string
    testimonialName: string
    testimonialUserHandle: string
    testimonialAvatar: StaticImageData,
    testimonialAvatarAlt: string
}

export default function TestimonialCard({ description, testimonialAvatar, testimonialAvatarAlt, testimonialName, testimonialUserHandle }: TTestimonialCard) {
    return <Card className="w-[320px] text-sm pt-3 h-[200px]">
        <CardContent>
            <p>{description}</p>
        </CardContent>
        <CardFooter className="flex items-center gap-3 py-3">
            <div>
                <Image src={testimonialAvatar} alt={testimonialAvatarAlt} height={40} width={40} />
            </div>
            <div className="flex flex-col">
                <span className="text-base font-semibold">{testimonialName}</span>
                <span className="text-xs font-normal text-gray-600">{testimonialUserHandle}</span>
            </div>
        </CardFooter>
    </Card>
}
```
