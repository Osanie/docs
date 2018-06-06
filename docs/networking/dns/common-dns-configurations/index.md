---
author:
  name: Linode
  email: docs@linode.com
description: 'Configurations for common DNS records.'
og_description: 'This guide explains how to use the Linode DNS manager, to configure DNS records'
keywords: ["dns"]
license: '[CC BY-ND 4.0](https://creativecommons.org/licenses/by-nd/4.0)'
aliases: ['dns-manager/','dns-guides/configuring-dns-with-the-linode-manager/']
modified: 2018-05-22
modified_by:
  name: Linode
published: 2015-01-20
title: Common DNS Configurations
---

![Common DNS Configurations](common-dns-configurations-title-graphic.jpg "Common DNS Configurations")

## Set Up a Domain

The most common DNS configuration is a single domain name on a single Linode. For this, you'll need to add *SOA* and *NS records* for all of your name servers, and *A/AAAA* records for your domain names. Use the screenshot below as a guide.

[![The SOA record is set to "ns1.linode.com". The NS records are set to "ns1.linode.com" through "ns5.linode.com", inclusive. The MX record is set to "mail.example.org". There are A records for [blank], which is the primary domain, and the "mail" and "www" subdomains. They are all set to the same IP.](1121-dns9.png)](1121-dns9.png)

 {{< note >}}
The DNS Manager can automatically add all of these records when you create a domain zone. For instructions, see [Adding Domain Zones](/docs/networking/dns/dns-manager#add-a-domain-zone) in the [DNS Manager](/docs/networking/dns/dns-manager) guide.
{{< /note >}}

## Configure Subdomains

To configure a subdomain, such as `staging.example.org`, create an A record with the subdomain's hostname. Point the record at the IP address of the server you want to host the subdomain:

[![Create a new A record, following the instructions in the "Adding" section. Add the subdomain text to the "Hostname" field. For example, you could type "staging" - NOT "staging.example.org".](1125-dns13.png)](1125-dns13.png)

## Host Multiple Domains on a Single Server

To host multiple domain names on a single server, create a separate domain zone for each domain name as shown below. When creating the new domain zones, we recommend that you allow the DNS Manager to automatically [insert basic records](/docs/networking/dns/dns-manager#add-a-domain-zone). At a minimum, you'll need an A record for each domain name pointing to the server's IP address.

[![This page shows the DNS Manager tab with three different domain zones listed.](1126-dns15.png)](1126-dns15.png)

## Use One Domain on Multiple Servers

If you have more than one server, but only one domain name, you can point A records with server-specific hostnames to all servers that need domain names. One machine will be the "front end" for the domain, by virtue of the first-level domain's A record pointing to it, but the domain can serve as a proxy for services provided by other machines if needed. For example, if you wanted to create a development environment on another server, you could create an A record for `staging.example.org` and point it at another Linode's IP address.

## Route Email to Third-Party Mail Services

To route email to a third-party email service, create MX records that associate your mail server (for example, `mail.example.org`) with a *hostname* provided by the third-party service. For instructions, see the website of your third-party email service.

## Use Wildcard DNS Records

A *wildcard* DNS record matches requests for non-existent domain names. For example, if you create an A record for `*.example.org`, and a user visits `nonexistantname.example.org`, that user will be redirected to `example.org`. An example wildcard DNS record is shown below.

[![Create a new A record, following the instructions in the "Adding" section. Add a single asterisk (\*) in the "Hostname" field. Set your IP address in the "IP Address" field. Then click the "Save Changes" button.](1127-dns16.png)](1127-dns16.png)