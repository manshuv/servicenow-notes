# ServiceNow Access Control Rules (ACLs)

Access Control Rules (ACLs) in ServiceNow are used to control access to records, fields, and tables. They determine what users can and cannot do with data in the system.

## Types of ACLs

### Record ACLs
Control access to entire records
- `read` - Can view the record
- `write` - Can edit the record
- `delete` - Can delete the record
- `create` - Can create new records

### Field ACLs
Control access to specific fields
- `read` - Can view the field
- `write` - Can edit the field

### UI ACLs
Control access to UI elements
- `read` - Can view the UI element
- `write` - Can modify the UI element

## ACL Conditions

ACLs can be configured with various conditions:

### User Role Conditions
- `current.user_has_role('itil')` - Checks if user has specific role
- `gs.hasRole('itil')` - Alternative syntax for role checks

### Record Conditions
- `current.active == true` - Checks record status
- `current.category == 'incident'` - Checks field values

### Field Conditions
- `current.short_description.length > 0` - Checks field content
- `gs.getUserID() == current.sys_created_by` - Checks record ownership

## Best Practices

1. **Least Privilege**
   - Grant only necessary permissions
   - Start with restrictive rules and add permissions as needed

2. **Role-Based Access**
   - Use roles instead of individual user checks
   - Group permissions logically

3. **Documentation**
   - Document purpose of each ACL
   - Maintain a list of affected tables and fields

4. **Testing**
   - Test ACLs thoroughly
   - Check edge cases
   - Verify permissions in different scenarios

## Common Use Cases

### Incident Management
```javascript
// Prevent non-admins from deleting incidents
if (gs.hasRole('admin')) {
    return true;
}
return false;
```

### Field Protection
```javascript
// Restrict access to sensitive fields
if (gs.hasRole('itil')) {
    return true;
}
return false;
```

### Record Level Security
```javascript
// Restrict access to specific records
if (current.active == true && gs.hasRole('itil')) {
    return true;
}
return false;
```

## Troubleshooting

1. **Debugging ACLs**
   - Use `gs.info()` for logging
   - Test with different user roles
   - Check system logs

2. **Common Issues**
   - ACLs not applying - Check conditions
   - Permission denied - Verify roles
   - Inconsistent access - Check field-level ACLs

## Security Considerations

1. **Data Protection**
   - Sensitive data - Use encryption
   - PII - Follow privacy regulations
   - Audit trails - Enable logging

2. **Performance**
   - Avoid complex conditions
   - Use indexes for frequently queried fields
   - Cache results when possible

## References

- [ServiceNow Documentation - ACLs](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/security/concept/c_AccessControlRules.html)
- [Best Practices for ACLs](https://docs.servicenow.com/bundle/paris-platform-administration/page/administer/security/reference/r_BestPracticesForACLs.html)
