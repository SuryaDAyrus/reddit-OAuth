# Reddit Integration for Xyopst Social Platform

## Overview

Xyopst Social is a social media management platform that allows users to connect and manage multiple social media accounts from a single interface.

Our Reddit integration enables users to:

* Connect their Reddit account through OAuth 2.0
* Read Reddit account information
* Retrieve subreddit information
* Create and manage Reddit posts
* Schedule Reddit content
* Manage Reddit advertising campaigns
* Access Reddit Ads reporting and campaign management tools

All Reddit actions are performed only after explicit OAuth authorization from the account owner.

---

# Why We Use Two Reddit Applications

Reddit currently separates Ads API permissions from standard Reddit OAuth permissions.

Because of this restriction, our platform uses two independent Reddit applications.

## Application 1: Reddit Content Management App

Purpose:

* User authentication
* Account connection
* Reading subreddit information
* Reading account information
* Creating posts
* Editing posts
* Managing content

Requested scopes:

* identity
* read
* submit
* edit
* history
* privatemessages
* mysubreddits
* modconfig

Example use cases:

### Account Connection

A user connects their Reddit account to Xyopst Social.

### Profile Retrieval

The platform retrieves:

* username
* profile image
* account metadata

using:

GET /api/v1/me

### Subreddit Discovery

The platform retrieves subreddit information associated with the authenticated account.

### Post Publishing

A user creates content inside Xyopst Social and publishes that content to Reddit using their own authorized account.

### Scheduled Publishing

A user schedules a post for future publication.

The platform publishes the content only on behalf of the authenticated user.

---

## Application 2: Reddit Ads App

Purpose:

* Reddit Ads campaign management
* Campaign reporting
* Ad account management
* Performance analytics

Requested scopes:

* adsread
* adsedit

Example use cases:

### Campaign Management

Users can:

* create campaigns
* edit campaigns
* pause campaigns
* activate campaigns

### Reporting

Users can view:

* impressions
* clicks
* spend
* conversions
* campaign performance metrics

through Reddit Ads APIs.

---

# Architecture

## OAuth Flow

### Content Management OAuth

1. User clicks "Connect Reddit"
2. User is redirected to Reddit OAuth
3. User grants authorization
4. Reddit returns authorization code
5. Platform exchanges authorization code for access token
6. Platform retrieves user profile
7. Tokens are securely stored
8. User can begin using Reddit publishing features

### Ads OAuth

1. User clicks "Connect Reddit Ads"
2. User is redirected to Reddit OAuth
3. User grants Ads permissions
4. Reddit returns authorization code
5. Platform exchanges authorization code for access token
6. Ads tokens are securely stored separately
7. User can begin using Ads functionality

---

# Token Storage

The platform stores OAuth credentials securely.

Content OAuth tokens and Ads OAuth tokens are stored separately.

Example structure:

```json
{
  "tokens": {
    "essentials": {
      "access_token": "...",
      "refresh_token": "..."
    },
    "ads": {
      "access_token": "...",
      "refresh_token": "..."
    }
  }
}
```

Each token is used only for APIs associated with its corresponding Reddit application.

---

# Security

The platform follows standard OAuth 2.0 practices:

* Authorization Code Flow
* Permanent refresh tokens
* Secure token storage
* User consent required
* No credential collection
* No password storage

Users may revoke access directly through Reddit at any time.

---

# User Authorization

Every Reddit action is performed only after the user explicitly authorizes access through Reddit OAuth.

The platform never performs actions on behalf of users who have not granted authorization.

---

# Anti-Spam Policy

This application is not designed for:

* Spam posting
* Vote manipulation
* Comment manipulation
* Automated engagement farming
* Unauthorized scraping
* Circumventing subreddit rules

The platform is intended solely for legitimate social media management and advertising workflows.

---

# Example Workflow

1. User connects Reddit account.
2. User creates a post inside Xyopst Social.
3. User selects a target subreddit.
4. User schedules or publishes the post.
5. Reddit receives the request through the user's OAuth authorization.
6. The content appears under the user's Reddit account.

---

# Intended Users

* Businesses
* Marketing teams
* Community managers
* Content creators
* Advertisers

---

# Contact

Platform: Xyopst Social

Developer Contact:

[surya.nagaraj@xyopst.ca](mailto:surya.nagaraj@xyopst.ca)

Purpose:

Reddit content publishing, subreddit management, and Reddit Ads campaign management through user-authorized OAuth integrations.
