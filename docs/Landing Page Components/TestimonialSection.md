---
sidebar_position: 3
---

# Testimonial Section

Testimonial Section is a section to show all you user testimonials in you landing page<br /><br />
![Testimonial Card](/img/testimonial-section.png)<br />
[View Live Example Here](https://rangoli-ui-live-components.vercel.app/testimonial-section)

## Does this depend on any other rangoli components?

Yes, Testimonial Section depend on Testimonial Card, Visit<br />
[Testimonial Card Component Guide](/docs/Landing%20Page%20Components/TestimonialCard)<br />

## Usage

```tsx
<TestimonialSection/>
```

## Component Code
```tsx
//Run The following command to install required shadcn component
//npx shadcn@latest add card

//put your avatar images on /src/assets folder
import avatar1 from "@/app/assets/avatar-1.png";
import avatar2 from "@/app/assets/avatar-2.png";
import avatar3 from "@/app/assets/avatar-3.png";
import avatar4 from "@/app/assets/avatar-4.png";
import avatar5 from "@/app/assets/avatar-5.png";
import avatar6 from "@/app/assets/avatar-6.png";
import avatar7 from "@/app/assets/avatar-7.png";
import avatar8 from "@/app/assets/avatar-8.png";
import avatar9 from "@/app/assets/avatar-9.png";
import TestimonialCard from "./TestimonialCard";
import { useI18n } from "../providers/i18nProvider";

export default function TestimonialSection() {
    const {t} = useI18n()

    const testimonialData = [
        { description: `${t("testimonial-1")}`, testimonialAvatar: avatar1, testimonialName: "Alex Carter", testimonialUserHandle: "@alexdev" },
        { description: `${t("testimonial-2")}`, testimonialAvatar: avatar2, testimonialName: "Samantha Lee", testimonialUserHandle: "@samanthadesign" },
        { description: `${t("testimonial-3")}`, testimonialAvatar: avatar3, testimonialName: "Daniel Brown", testimonialUserHandle: "@danbrowncode" },
        { description: `${t("testimonial-4")}`, testimonialAvatar: avatar4, testimonialName: "Nina Patel", testimonialUserHandle: "@ninapatelux" },
        { description: `${t("testimonial-5")}`, testimonialAvatar: avatar5, testimonialName: "Liam Johnson", testimonialUserHandle: "@liam_js" },
        { description: `${t("testimonial-6")}`, testimonialAvatar: avatar6, testimonialName: "Emma Wilson", testimonialUserHandle: "@emmawilsonui" },
        { description: `${t("testimonial-7")}`, testimonialAvatar: avatar7, testimonialName: "Chris Adams", testimonialUserHandle: "@chrisux" },
        { description: `${t("testimonial-8")}`, testimonialAvatar: avatar8, testimonialName: "Sophia Martinez", testimonialUserHandle: "@sophiamdesign" },
        { description: `${t("testimonial-9")}`, testimonialAvatar: avatar9, testimonialName: "Ethan Reynolds", testimonialUserHandle: "@ethanreact" }
    ];

    // Split testimonials into three columns
    const columns = [
        testimonialData.slice(0, 3), // First column
        testimonialData.slice(3, 6), // Second column
        testimonialData.slice(6, 9), // Third column
    ];

    return (
        <section>
            <h1 className="text-4xl font-medium text-center">{t("what-users-are-saying")}</h1>
            <div className="flex justify-center gap-10 mt-20">
                {columns.map((column, columnIndex) => (
                    <div 
                        key={columnIndex}
                        className={`
                            flex flex-col gap-8 
                            ${columnIndex === 1 ? "hidden md:flex" : ""}  // Show second column on md+
                            ${columnIndex === 2 ? "hidden lg:flex" : ""}  // Show third column on lg+
                        `}
                    >
                        {column.map((testimonial, index) => (
                            <TestimonialCard
                                key={index}
                                description={testimonial.description}
                                testimonialAvatar={testimonial.testimonialAvatar}
                                testimonialAvatarAlt={`Avatar ${index}`}
                                testimonialName={testimonial.testimonialName}
                                testimonialUserHandle={testimonial.testimonialUserHandle}
                            />
                        ))}
                    </div>
                ))}
            </div>
        </section>
    );
}
```
