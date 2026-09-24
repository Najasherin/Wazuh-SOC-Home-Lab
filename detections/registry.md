# Windows Registry Monitoring

## Objective

Test Windows Registry Integrity Monitoring using Wazuh Syscheck.

## Registry Monitoring

The Windows Wazuh Agent included registry monitoring for Windows Registry locations including:

```text
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Run
```

## Temporary Scan Frequency

The normal FIM frequency was:

```text
43200 seconds
```

For lab testing, it was temporarily changed to:

```text
300 seconds
```

After testing, it was restored to:

```text
43200 seconds
```

## Registry Test

A temporary Run value was created:

```text
WazuhTest
```

The registry value was later removed.

Registry integrity events were observed in Wazuh.

The specific `WazuhTest` value did not produce the expected Threat Hunting search result, so it is not presented as a successful direct alert.

## Cleanup

The temporary registry value was deleted and the original FIM frequency was restored.

## Result

Registry integrity monitoring was successfully observed, while the specific Run-key detection test did not produce the expected search result.
