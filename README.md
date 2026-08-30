[![](https://img.shields.io/nuget/v/soenneker.extensions.timezoneinfos.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.extensions.timezoneinfos/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.extensions.timezoneinfos/publish-package.yml?style=for-the-badge)](https://github.com/soenneker/soenneker.extensions.timezoneinfos/actions/workflows/publish-package.yml)
[![](https://img.shields.io/nuget/dt/soenneker.extensions.timezoneinfos.svg?style=for-the-badge)](https://www.nuget.org/packages/soenneker.extensions.timezoneinfos/)
[![](https://img.shields.io/github/actions/workflow/status/soenneker/soenneker.extensions.timezoneinfos/codeql.yml?label=CodeQL&style=for-the-badge)](https://github.com/soenneker/soenneker.extensions.timezoneinfos/actions/workflows/codeql.yml)

# ![](https://user-images.githubusercontent.com/4441470/224455560-91ed3ee7-f510-4041-a8d2-3fc093025112.png) Soenneker.Extensions.TimeZoneInfos
Map the four continental US time-zone IDs to stable, daylight-agnostic abbreviations.

## Installation

```bash
dotnet add package Soenneker.Extensions.TimeZoneInfos
```

## Usage

```csharp
using Soenneker.Extensions.TimeZoneInfos;

TimeZoneInfo timeZone = TimeZoneInfo.FindSystemTimeZoneById("America/Chicago");
string abbreviation = timeZone.ToSimpleAbbreviation(); // "CT"
```

The mapping recognizes both Windows and IANA identifiers:

| Windows ID | IANA ID | Result |
| --- | --- | --- |
| `Eastern Standard Time` | `America/New_York` | `ET` |
| `Central Standard Time` | `America/Chicago` | `CT` |
| `Mountain Standard Time` | `America/Denver` | `MT` |
| `Pacific Standard Time` | `America/Los_Angeles` | `PT` |

The comparison is case-insensitive. Other zones return `"Unknown"`.

The result deliberately does not distinguish standard time from daylight time: New York returns `ET`, not `EST` or `EDT`. This method does not inspect an instant or calculate an offset; use `TimeZoneInfo.GetUtcOffset()` when the date-specific offset matters.
