How do I create an endpoint?
---
/*
 * The [.arguments] node is MANDATORY for an HTTP endpoint since without it, any argument can
 * be submitted to it, which would be a security risk.
 * Hence, when creating HTTP endpoints then ALWAYS add a [.arguments] node at the top, just
 * below the file level comment if there is one.
 */
.arguments
