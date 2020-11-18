---
published: false
---
## Introduction
Introduce concept here
## Laying the groundwork

### Issues
 
Talk about issues I came across, listed in my notes.txt
handle was dropped when calling into_raw()
shared mem file isn't being deleted at the end of the program due to panic: swapped to nanomsg
panicking because WSAStartup isn't being called: fixed via ghost bind -- no longer needed due to WSA calls during socket hand off
hanging on sending/receiving from pipe: had to call dial/listen
handle table needs duplication: wsaduplicatesocket
will fail if run as admin for parent
doesn't handle elevation request being denied

```rust
impl From<WSAPROTOCOL_INFOA> for WSAProcessInfo {
    fn from(info: WSAPROTOCOL_INFOA) -> Self {
        let sz_protocol = info.szProtocol.iter().map(|&c| c as u8).collect();
        // WinAPI should provide valid ASCII, which is also valid UTF-8
        let sz_protocol = String::from_utf8(sz_protocol).unwrap(); 

        Self {
            service_flags: [
                info.dwServiceFlags1,
                info.dwServiceFlags2,
                info.dwServiceFlags3,
                info.dwServiceFlags4,
                info.dwServiceFlags5,
            ],
            provider_id: info.ProviderId.into(),
            catalogue_entry_id: info.dwCatalogEntryId,
            protocol_chain: info.ProtocolChain.into(),
            version: info.iVersion,
            address_family: info.iAddressFamily,
            max_sock_addr: info.iMaxSockAddr,
            min_sock_addr: info.iMinSockAddr,
            socket_type: info.iSocketType,
            i_protocol: info.iProtocol,
            protocol_max_offset: info.iProtocolMaxOffset,
            network_byte_order: info.iNetworkByteOrder,
            security_scheme: info.iSecurityScheme,
            message_size: info.dwMessageSize,
            provider_reserved: info.dwProviderReserved,
            sz_protocol,
        }
    }
}
```
