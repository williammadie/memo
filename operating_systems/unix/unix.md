# UNIX

## Table of Contents

- [UNIX VS Linux](#unix-vs-linux)
- [Difference of usage between UNIX and Linux](#difference-of-usage-between-unix-and-linux)
- [UNIX and Linux similarities](#unix-and-linux-similarities)
    - [Process Tree Structure](#process-tree-structure)
- [UNIX strftime](#unix-strftime-string-formatter-for-datetime)

## UNIX VS Linux

In a nutshell:

(found on the web)

Linux is nothing but a UNIX clone which is written Linus Torvalds from scratch with the help of some hackers across the globe.

UNIX and UNIX-like operating systems are a family of computer operating systems that derive from the original UNIX System from Bell Labs which can be traced back to 1965.

Most famous **UNIX-based/UNIX-like operating systems** are `Linux` and `macOS`.

In details:

UNIX was initially developed for mainframes and was later ported to minicomputers and then to personal computers. It is widely used for server and enterprise applications, as well as for scientific and academic purposes.

Linux, on the other hand, was developed as a free alternative to UNIX and has since become popular for personal computers, servers, and mobile devices. One of the biggest differences between UNIX and Linux is that UNIX is proprietary and licensed, while Linux is open-source and freely available.

In terms of functionality, both UNIX and Linux provide similar basic services, such as file management, process management, and communication between processes. However, Linux has a larger community of developers, resulting in a more active development cycle and a wider range of available software.

In conclusion, while UNIX and Linux are similar in many ways, Linux is a free, open-source operating system based on the UNIX operating system, and has a larger community of developers and more available software.

## Difference of usage between UNIX and Linux

(The text below is the answer of ChatGPT)

Linux and UNIX are both widely used operating systems, each with its own strengths and areas of use. Here are some examples of who uses each and for what purpose:

UNIX:

    Enterprises and organizations: UNIX is widely used in enterprise environments for mission-critical applications, such as financial systems, databases, and customer relationship management systems.
    Scientific and academic institutions: UNIX is also used in scientific and academic environments for high-performance computing and data analysis.
    Government agencies: UNIX is used by many government agencies for secure and reliable computing.

Linux:

    Web servers: Linux is widely used as the operating system for web servers, due to its stability, security, and scalability.
    Embedded systems: Linux is also used in embedded systems, such as mobile devices, smart TVs, and home automation systems.
    Personal computers: Linux is a popular choice for personal computers, particularly among developers and tech-savvy users.
    Cloud computing: Linux is widely used as the operating system for cloud computing infrastructure, such as Amazon Web Services and Microsoft Azure.

It is worth noting that while UNIX and Linux have some similarities, they also have some differences in terms of features and functionality. For example, UNIX has a longer history and more mature ecosystem, but may be more expensive to use and maintain compared to Linux. On the other hand, Linux has a larger community of developers, a more active development cycle, and is freely available, making it a more cost-effective option for some users.

## UNIX and Linux similarities

## Process Tree Structure

In both systems, all processes have **a common ancestor** called the `init` process. It has a PID (Process IDentifier) equals to `1`.

All other processes are child or grandchild (and more) of the `init` process.

Below is a screenshot taken on an Ubuntu system
![process-structure](/operating_systems/unix/resources/process-tree-structure.png)

## UNIX strftime (String formatter for Datetime)

Some common formats:

- `%d-%m-%Y`: 21-04-2022
- `%A, %B %e, %Y`: Sunday, June 5, 2015
- `%b %e %a`: Jun 5 Sun
- `%H:%M:%S`: 14:03:12
- `%I:%M %p`: 11:05 PM

Date formats

- `%a`: sun
- `%A`: Sunday
- `%w`: weekday number (0 - 6)
- `%y`: 13
- `%Y`: 2013
- `%b`: Jan
- `%B`: January
- `%m`: month number (01 - 12)
- `%d`: day number in month (01 - 31)
- `%e`: day number in month (int formatted) (1 - 31)

Time formats

- `%l`: Hour (int formatted) (1 - 24)
- `%H`: 24h Hour (00 - 23)
- `%I`: 12h Hour (01 - 12)
- `%M`: Minutes (00 - 59)
- `%S`: Seconds (00 - 60)
- `%p`: AM or PM
- `%Z`: Timezone (ex: +08)
- `%j`: Day of the year (001 - 366)
- `%%`: Litteral `%` character