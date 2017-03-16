---
title: Active Directory 身份验证协议 | Azure
description: 本文概述 Azure Active Directory 支持的各种身份验证和授权协议。
services: active-directory
documentationCenter: .net
authors: priyamohanram
manager: mbaldwin
editor: ''

ms.service: active-directory
ms.date: 06/06/2016
wacn.date: 02/06/2017
---

# Active Directory 身份验证协议

Azure Active Directory (Azure AD) 支持多个最广泛使用的身份验证和授权协议。

在本系列文章中，我们将探讨支持的协议及其在 Azure AD 中的实现。我们将提供示例请求和响应。由于我们要直接与协议集成，因此这些文章基本上与语言无关。

- [OAuth 2.0 授权代码授予](./active-directory-protocols-oauth-code.md)：了解 OAuth2.0 的“授权代码”授予及其在 Azure AD 中的实现。
- [OAuth 2.0 隐式授权](./active-directory-dev-understanding-oauth2-implicit-grant.md)：了解 OAuth 2.0 的“隐式”授权，以及它是否适合你的应用程序。
- [OpenID Connect 1.0](./active-directory-protocols-openid-connect-code.md)：了解如何在 Azure AD 中使用 OpenID Connect 身份验证协议。
- [SAML 协议参考](./active-directory-saml-protocol-reference.md)：了解如何使用 SAML 协议来支持 Azure AD 中的[单一登录](./active-directory-single-sign-on-protocol-reference.md)和[单一注销](./active-directory-single-sign-out-protocol-reference.md)。

## 参考和故障排除

本文章系列提供的附加信息可能对排查 Azure AD 应用程序问题有所作用，并可以帮助你深入了解 Azure AD。

- [联合元数据](./active-directory-federation-metadata.md)：了解如何查找和解释 Azure AD 生成的元数据文档。
- [支持的令牌和声明类型](./active-directory-token-and-claims.md)：了解 Azure AD 颁发的令牌中的各种声明。
- [Azure AD 中的签名密钥滚动更新](./active-directory-signing-key-rollover.md)：了解 Azure AD 的签名密钥滚动更新频率，以及如何为最常见的应用程序方案更新密钥。
- [排查身份验证协议问题](./active-directory-error-handling.md)：了解如何解释和解决在使用 OAuth 2.0 和 Azure AD 时遇到的最常见错误。
- [Azure AD 中 OAuth 2.0 的最佳实践](./active-directory-oauth-best-practices.md)：了解在 Azure AD 中使用 OAuth 2.0 时可以运用的最佳实践，以及如何避免常见错误。

<!---HONumber=Mooncake_Quality_Review_0125_2017-->