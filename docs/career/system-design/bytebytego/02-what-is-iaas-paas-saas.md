---
date:
  created: 2023-11-30
  updated: 2023-11-30

description: >
  Insight about "What is IaaS/PaaS/SaaS?"

tags:
  - System Design
  - ByteByteGo

comments: true
---
# What is IaaS/PaaS/SaaS?

<figure markdown>
  ![comparison](https://www.redhat.com/rhdc/managed-files/iaas-paas-saas-diagram5.1-1638x1046.png)
  <figcaption>Comparison of traditional, IaaS, PaaS and SaaS</figcaption>
</figure>

The above figure is the visual [comparison](https://www.redhat.com/en/topics/cloud-computing/iaas-vs-paas-vs-saas) of traditional, IaaS, PaaS and SaaS over different levels from hardware to software.

## Service Providers

Since the figure had told everything, I would like to provide some exmples of these service providers.

### IaaS

IaaS has basically handled all hardware related problems that companies may face traditionally. The well known companies include:

1. Amazon Web Service Elastic Compute Cloud (AWS EC2): has the largest market share and starts the earliest.
2. Google Compute Engine (GCE): one of the service provided by Google Cloud Platform (GCP), easy to use.
3. Digital Ocean: never tried their services but read a bunch of their technical articles, extremely helpful❤️😂.

Others like **Azure**, **linode** are also very popular. [Source](https://www.g2.com/categories/infrastructure-as-a-service-iaas)

### PaaS

PaaS further handles the build & deploy to let users focus on the APP development part. However, it means that your APP development may depends on the runtime environment in other words. The observability, stability, usability and other metrics are also important considerations when choosing the service provider. Here are common providers:

1. Google App Engine
2. Amazon Elastic Beanstalk
3. Azure App Service
4. Heroku

I've tried App Engine and Heroku before and I like both of them for the ease of use. [Source](https://www.techradar.com/news/best-paas-provider)

### SaaS

There are many SaaS companies out there such as Slack, Notion, Docker, Zoom and other daily use apps (as a software engineer). I won't list them here since the list is too long. Instead, you may go [there](https://www.datamation.com/cloud/saas-companies/) to see some well-known companies.