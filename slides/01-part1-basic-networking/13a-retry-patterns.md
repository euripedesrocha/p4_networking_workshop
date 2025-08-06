# Smart Retry: Network Instability Patterns

<div class="grid grid-cols-2 gap-8">

<div>

### Temporary Issues (Should Retry)
- **Signal interference**: Temporary radio congestion
- **AP overload**: Too many clients connecting
- **DHCP delays**: Slow IP address assignment
- **Roaming**: Moving between access points

### Permanent Issues (Should NOT Retry)
- **Wrong password**: Authentication will keep failing
- **Security mismatch**: Incompatible encryption
- **MAC filtering**: Device blocked by AP
- **Hidden network**: SSID not found

</div>

<div>

### Decision Strategy

**Rule of thumb**: If the problem is likely to resolve itself (signal, congestion, timing), retry. If it's a configuration issue (credentials, security), don't spam the network.

</div>

</div>
