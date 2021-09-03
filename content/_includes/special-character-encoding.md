### Special characters encoding

The adapter encodes special characters used in the **StreamId** parameter string before sending it to configured endpoints. The adapter substitutes the following encoded characters for special characters:

| Special character | Encoded character |
|--|--|
| `*` | character omitted |
| `'` | character omitted |
| <code>`</code> | character omitted |
| `"` | character omitted |
| `?` | character omitted |
| `;` | `-` |
| `\| ` | `-` |
| `\` | character omitted |
| `{` | `(` |
| `}` | `)` |
| `[` | `(` |
| `]` | `)` |