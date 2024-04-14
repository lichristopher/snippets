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

### Dynamic Route handlers in next js

```tsx
import { comments } from '../data';

//Get Request
export async function GET(
  _request: Request,
  {
    params,
  }: {
    params: {
      id: string;
    };
  }
) {
  const comment = comments.find((comment) => {
    return comment.id === parseInt(params.id);
  });

  return Response.json(comment);
}

// Patch Request
export async function PATCH(
  request: Request,
  {
    params,
  }: {
    params: {
      id: string;
    };
  }
) {
  const body = await request.json();
  const { text } = body;
  const index = comments.findIndex((comment) => {
    return comment.id === parseInt(params.id);
  });
  comments[index] = text;
  return Response.json(comments[index]);
}

export async function DELETE(
  request: Request,
  {
    params,
  }: {
    params: {
      id: string;
    };
  }
) {
  const index = comments.findIndex((comment) => {
    return comment.id === parseInt(params.id);
  });

  const deletedComment = comments[index];
  comments.splice(index, 1);
  return Response.json(deletedComment);
}
```
