# Adguard DNS blocklists

Based on https://github.com/AdguardTeam/HostlistCompiler

## <a name="usage"></a> Usage

Install dependencies
```bash
npm i -g @adguard/hostlist-compiler
```

Compile fresh list
```bash
hostlist-compiler -c blocklist/basic.json -o basic.txt
```

### <a name="configuration"></a> Configuration

Configuration defines your filter list sources, and the transformations that are applied to the sources.

Here is an example of this configuration:

```json
{
  "name": "List name",
  "description": "List description",
  "homepage": "https://example.org/",
  "license": "GPLv3",
  "sources": [
    {
      "name": "Local rules",
      "source": "rules.txt",
      "type": "adblock",
      "transformations": ["RemoveComments", "Compress"],
      "exclusions": ["excluded rule 1"],
      "exclusions_sources": ["exclusions.txt"],
      "inclusions": ["*"],
      "inclusions_sources": ["inclusions.txt"]
    },
    {
      "name": "Remote rules",
      "source": "https://example.org/rules",
      "type": "hosts",
      "exclusions": ["excluded rule 1"]
    }
  ],
  "transformations": ["Deduplicate", "Compress"],
  "exclusions": ["excluded rule 1", "excluded rule 2"],
  "exclusions_sources": ["global_exclusions.txt"],
  "inclusions": ["*"],
  "inclusions_sources": ["global_inclusions.txt"]
}
```

- `name` - (mandatory) the list name.
- `description` - (optional) the list description.
- `homepage` - (optional) URL to the list homepage.
- `license` - (optional) Filter list license.
- `sources` - (mandatory) array of the list sources.
  - `.source` - (mandatory) path or URL of the source. It can be a traditional filter list or a hosts file.
  - `.name` - (optional) name of the source.
  - `.type` - (optional) type of the source. It could be `adblock` for Adblock-style lists or `hosts` for /etc/hosts style lists. If not specified, `adblock` is assumed.
  - `.transformations` - (optional) a list of transformations to apply to the source rules. By default, **no transformations** are applied. Learn more about possible transformations [here](#transformations).
  - `.exclusions` - (optional) a list of rules (or wildcards) to exclude from the source.
  - `.exclusions_sources` - (optional) a list of files with exclusions.
  - `.inclusions` - (optional) a list of wildcards to include from the source. All rules that don't match these wildcards won't be included.
  - `.inclusions_sources` - (optional) a list of files with inclusions.
- `transformations` - (optional) a list of transformations to apply to the final list of rules. By default, **no transformations** are applied. Learn more about possible transformations [here](#transformations).
- `exclusions` - (optional) a list of rules (or wildcards) to exclude from the source.
- `exclusions_sources` - (optional) a list of files with exclusions.
- `.inclusions` - (optional) a list of wildcards to include from the source. All rules that don't match these wildcards won't be included.
- `.inclusions_sources` - (optional) a list of files with inclusions.
