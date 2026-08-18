# AWS Critical Thinking Project: Reverse Proxy for Two Company Websites

**Author:** Adeniyi Abdulazeez (`hayzeddev123`)  
**Date:** August 2026

---

## 1. Introduction

This project focuses on deploying two company websites on AWS using reverse proxy technology to improve security, performance, scalability, and cost efficiency.

The first website is an **e-commerce platform** that handles sensitive customer information.  
The second is a **CMS website** used for articles and blogs.

---

## 2. Proposed Architecture

Both websites will use a reverse proxy as an additional layer between users and the application servers.

**Architecture Diagram (created with draw.io):**

![Reverse Proxy Architecture](reverse-proxy.drawio.png)

```
                    Internet
                       |
                Load Balancer
                       |
              Reverse Proxy
             /             \
      E-Commerce          CMS Website
          |                   |
       EC2 Servers          EC2 Servers
          |                   |
         RDS              Database
```

---

## 3. Reverse Proxy Implementation

The reverse proxy can be implemented using **NGINX on Amazon EC2**.

It will:

* Receive requests from users.
* Forward requests to the appropriate web servers.
* Filter unwanted traffic.
* Cache frequently requested content.
* Hide the private IP addresses of backend servers.
* Help distribute traffic between multiple servers.

---

## 4. E-Commerce Website

Because the e-commerce website handles sensitive customer information, stronger security should be applied.

The architecture should use:

* **HTTPS/TLS** for encrypted communication.
* **AWS WAF** to filter malicious web requests.
* **Security Groups** to restrict access.
* **Private subnets** for application servers and databases.
* **Amazon RDS** for the database.
* **Auto Scaling** to handle changes in traffic.

Sensitive database resources should **not** be directly accessible from the internet.

---

## 5. CMS Website

The CMS website mainly serves articles, images, and other content.

The reverse proxy can use **caching** to store frequently requested content. This reduces requests reaching the backend servers and improves website performance.

Auto Scaling can also add or remove EC2 instances depending on traffic.

---

## 6. Scalability and High Availability

Both websites should use:

* **Elastic Load Balancer (ELB)** to distribute traffic.
* **Auto Scaling Groups** to automatically adjust the number of EC2 instances.
* **Multiple Availability Zones** to reduce downtime.
* **Health checks** to remove unhealthy servers from service.

```
              Load Balancer
              /           \
           AZ-A           AZ-B
            |               |
        Reverse Proxy   Reverse Proxy
            |               |
          EC2             EC2
```

---

## 7. Performance and Cost Optimization

* Reverse proxy caching reduces backend workload and improves response times.
* AWS Auto Scaling prevents paying for unnecessary servers during periods of low traffic while providing additional capacity during traffic spikes.
* Using RDS instead of managing database servers manually also reduces administrative overhead.

---

## 8. Conclusion

Reverse proxy technology provides an effective layer between users and backend applications. By combining **NGINX**, **ELB**, **Auto Scaling**, **EC2**, **RDS**, **WAF**, and **multiple Availability Zones**, both websites can achieve improved security, scalability, performance, and availability.

- The **e-commerce website** should prioritize security and protection of customer data.
- The **CMS website** should focus more heavily on caching and content delivery.

This approach provides a balanced AWS architecture while keeping resource usage and costs under control.

---

**End of Report**
