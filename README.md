# snippets

a repository for storing my coding snippets

## Snippets for Next js

### Route handlers in next js

```tsx
import { comments } from './data';
export async function GET() {
  return Response.json();
}

export async function POST(request: Request) {
  const comment = await request.json();
  const newComment = {
    id: comments.length + 1,
    text: comment.text,
  };
  comments.push(comment);
  return new Response(JSON.stringify(newComment), {
    headers: {
      'Content-type': 'application/json',
    },
    status: 201,
  });
}
```
