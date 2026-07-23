# Foundations Audit

Use AuditService for audit recording.

Example:

auditService.record(
    AuditAction.CREATE,
    "CUSTOMER",
    customerId
);

Do not create a custom audit table or custom audit framework when this
artifact provides the required capability.