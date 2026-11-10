# 🧪Quick Validation Checklist
## Verify DNS & Domain Connectivity

  - Run *ping 192.168.10.10* to confirm IP reachability.

  - Run *nslookup lab.local* for DNS Check. If it shows 192.168.10.10, you're good.

## Verify User & Group Memberships

Run *whoami /groups* to ensure the logged-in user displays their designated OU security groups *(e.g., Sales_Users, IT_Admins)*
