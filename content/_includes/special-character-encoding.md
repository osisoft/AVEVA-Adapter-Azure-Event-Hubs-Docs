### Special characters encoding

The adapter encodes special characters used in the **StreamId** parameter string before sending it to configured endpoints. The adapter substitutes the following encoded characters for special characters:

| Special character | Encoded character |
|--|--|
| `*` | empty space |
| `'` | empty space |
| <code>`</code> | empty space |
| `"` | empty space |
| `?` | empty space |
| `;` | `-` |
| `\| ` | `-` |
| `\` | empty space |
| `{` | `(` |
| `}` | `)` |
| `[` | `(` |
| `]` | `)` |