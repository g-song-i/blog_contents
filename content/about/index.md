---
title: "Songi's Technical Diary"
date: 2023-04-08
summary: ""
layout: about
---

Hi, I am Songi 😊

My favorite quote: Between stimulus and response there is a space. In that space is our power to choose our reponse. In our response lies our growth and our freedom (Viktor E. Frankl). I always keep this in mind to remind me that I am the one who can manage and be responsible for myself. I try my best to be better in every aspect and not to regret what I've done. Though I think of myself as a wandering child nowadays, I hope I would be better.

For academic aspects, I've researched and studied **cloud-native security**, which can be described as container security, during my master's course. Among different phases of the container's lifecycle, I mainly focus on **runtime security** powered by **eBPF (extended Berkeley Packet Filter)**. eBPF is now widely used, so I guess everyone knows about it. Since it provides helpful observability to a system by attaching eBPF programs to the kernel's wide range of hookpoints, it can help a system administrator enforce specific actions when events occur as defined by eBPF programs. I've worked with eBPF by taking advantage of it for cloud-native security, especially runtime security. You can read my work below!

[Here's my github link!][github]

[github]: https://github.com/g-song-i

***

#### Doctoral Course, Soongsil University, Seoul, 06978, Republic of Korea
<small>2023.02 - now </small>

- Study in Information and Telecommunication Engineering Department, Communication and Network Security Laboratory

  - **Jornals**
    + ["Container Instrumentation and Enforcement System for Runtime Security of Kubernetes Platform with eBPF (Intelligent Automation & Soft Computing)"][journal3link]
      + This work is the extended version of the paper I wrote for the conference below. The paper basically uses **BPF-LSM** (a LSM implementation powered by eBPF) to enforce specific policies to a or a group of container. The policy will be provided in a YAML format, helping the admin make eBPF programs easily.

      [journal3link]: https://cdn.techscience.cn/files/iasc/2023/TSP_IASC-37-2/TSP_IASC_39565/TSP_IASC_39565.pdf

  - **Lecture Notes (Conference Paper Publication)**
    + ["MDagg: A New Aggregation Method Using Mahalanobis Distance"][lecturenote1link]
      + In this work, the target is a federated learning architecture. I suggest a new aggregation rule to avoid malicious gradients when aggregating by considering relations among gradients with **Mahalanobis distance, not just Euclidian distance**. But unfortunately, there is no specific equation since my math is terrible 🥲. I enjoy mathematical thinking, but it is hard to calculate exact answers than understand them intuitively. So I thought the idea was not that bad... but who knows 🤣 

      [lecturenote1link]: https://link.springer.com/chapter/10.1007/978-981-99-1252-0_5

#### Master's Degree, Soongsil University, Seoul, 06978, Republic of Korea
<small>2021.03 - 2023.02</small>

- Graduate Information and Telecommunication Engineering Department, Communication and Network Security Laboratory
- Most of my time during my master's course, I've focused on Cloud-native security. My work is as follows:
  (I am not the first author of all achievements, some of them might not. If you are intersted in some of my researches, please refer to the link and check 😎!)

  - **Jornals**
    + ["Implementation of Opensource-Based Automatic Monitoring Service Deployment and Image Integrity Checkers for Cloud-Native Environment (Journal of the Korea Institute of Information Security & Cryptology)"][journal2link]
      + In this work, I implement docker-compose environment to setup open-source container monitoring tool - which is **Falco**. I integrate monitoring system and some other tools to visualize matrix - which are **Prometheus and Grafana**. It's not an advanced work, I devloped how we deploy monitoring tools with docker more easily. ++ Image integrity check with **DCT (Docker Content Trust)**
  
      [journal2link]: http://koreascience.or.kr/article/JAKO202224951100631.page


  - **Patents**
    + ["METHOD OF ANALYZING CONTAINER SYSTEM CALL CONFIGURATION ERROR , AND RECORDING MEDIUM AND APPARATUS FOR PERFORMING THE SAME (US patent application publication)"][patent0link]

    [patent0link]: https://patentimages.storage.googleapis.com/6c/66/9d/11257067c9cf22/US20230008660A1.pdf

    + ["DOCKER IMAGE VULNERABILITY INSPECTION DEVICE AND METHOD FOR PERFORMING DOCKER FILE ANALYSIS (US patent application publication)"][patent1link]
  
    [patent1link]: https://patents.google.com/patent/US20220108023A1/
  
    + ["METHOD FOR ON-DEVICE ANDROID MALWARE DETECTION USING TRANSFER LEARNING BASED ADAPTIVE MODEL, RECORDING MEDIUM AND DEVICE FOR PERFORMING THE METHOD (Korea patent application publication)"][patent2link]
  
    [patent2link]: https://doi.org/10.8080/1020210073580
  
    + ["DESIGN METHOD FOR PROFILE SHARING IN CONTAINER ENVIRONMENT, RECORDING MEDIUM AND DEVICE FOR PERFORMING THE METHOD (Korea patent registration)"][patent3link]
  
    [patent3link]: https://doi.org/10.8080/1020210089527


  - **Conference Papers**
    + **_2022 Best Student Paper from KISTI_**, MobiSec Conference for my paper "KRSIE: An eBPF-based Kubernetes Runtime Security Instrumentation and Enforcement System"
- Basically, I work with **Docker and Kubernetes** environment on **Linux Ubuntu OS**. Thus, I have some basic knowledge for these systems. To make applications, I program with these languages: **C, python, and Golang**. Especially, I've tried to learn **eBPF technology**!


#### Bachelor Degree, Changwon National University, Changwon, 51140, Republic of Korea
<small>2017 - 2021.02</small>

- Graduate Computer Engineering Department.
- Since my major was computer engineering, I've learned a plethora of things encompassing all sorts of the computer knowledge overall. 
- I belonged to **"Computer Network Laboratory"**. In the lab, I've learn basic network knowledge including wireless network. I also joined a work with my lab members, the work is ["Time-Sensitive Networking Technologies for Industrial Automation in Wireless Communication Systems (Energies, 2021)"][journal1link]. 

[journal1link]: https://www.mdpi.com/1996-1073/14/15/4497

- I could say I've done two main projects during my undergraduate days.
  + **_Group matching application for study within university (Android Application)_**
    + In this project, I coded things related to server side stuff. I setup **Window server and Maria DB** built on the top of **AWS EC2 instance and RDS (Relational Database Service)**. I chose **PHP** as server side script language after testing some other things (PHP, JSP, and ASP). Moreover, I experienced implementing email verification service since the application only allows university students to use the app :) ++ **Java skills**
  + **_Trading used goods application based on block-chain technology (Android Application)_**
    + In this project, I also coded server side stuff. For this app, I setup **Ubuntu server with AWS EC2 instance** and I used **Node.js** server. For this project, I implemented SMS (Message service in Korea) verification service. Also, I setup local Ethereum network to deploy smart contract which will prove transaction of used goods in the future. 
- I got A+ on the subjects "Information Security" and "System Security", it is not a big task, but I'd had interests on security area through the classes at the very beginning.

## Certificates

- Language: English
  + TOEIC 870 (23.01.29)