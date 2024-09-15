# React Query - Full Guide

**React Query** is a powerful data-fetching and state management library for React applications. It helps simplify fetching, caching, synchronizing, and updating server-side data, with powerful features like caching, background fetching, and automatic retries.

## Installation

```bash
npm install react-query
npm install axios
```

> You can use any HTTP client, like `axios` or `fetch`, for making requests. Here, we use `axios` in the examples.

## Basic Setup

### 1. **Setting Up `QueryClient` and `QueryClientProvider`**

To start using React Query, wrap your app with the `QueryClientProvider` and pass a `QueryClient` instance.

```jsx
import { QueryClient, QueryClientProvider } from 'react-query';

const queryClient = new QueryClient();

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {/* Your application components */}
    </QueryClientProvider>
  );
}
```

---

## Fetching Data with `useQuery`

The `useQuery` hook is used to fetch data and manage its state, including loading, success, and error statuses.

```jsx
import { useQuery } from 'react-query';
import axios from 'axios';

const fetchPosts = async () => {
  const { data } = await axios.get('/api/posts');
  return data;
};

function Posts() {
  const { data, error, isLoading, isError, isFetching } = useQuery('posts', fetchPosts);

  if (isLoading) return <div>Loading...</div>;
  if (isError) return <div>Error: {error.message}</div>;

  return (
    <div>
      {isFetching && <div>Refreshing...</div>}
      <ul>
        {data.map(post => (
          <li key={post.id}>{post.title}</li>
        ))}
      </ul>
    </div>
  );
}
```

### Common `useQuery` Parameters:
- **Query Key**: A unique identifier for the query (e.g., `'posts'`).
- **Query Function**: The function that fetches the data (e.g., `fetchPosts`).
- **Options**: (optional) Configuration options, such as refetch behavior and caching.

```jsx
useQuery(['posts', userId], () => fetchPostsByUser(userId), { staleTime: 5000 });
```

---

## Mutating Data with `useMutation`

To modify data (e.g., POST, PUT, DELETE), use the `useMutation` hook. It allows you to trigger mutations and handle side effects, like cache invalidation.

```jsx
import { useMutation, useQueryClient } from 'react-query';

const createPost = async (newPost) => {
  const { data } = await axios.post('/api/posts', newPost);
  return data;
};

function CreatePost() {
  const queryClient = useQueryClient();
  const mutation = useMutation(createPost, {
    onSuccess: () => {
      queryClient.invalidateQueries('posts'); // Invalidate cache after a successful mutation
    }
  });

  const handleCreate = () => {
    mutation.mutate({ title: 'New Post' });
  };

  return (
    <div>
      <button onClick={handleCreate}>Create Post</button>
      {mutation.isLoading && <div>Creating...</div>}
      {mutation.isError && <div>Error: {mutation.error.message}</div>}
    </div>
  );
}
```

### `useMutation` Parameters:
- **Mutation Function**: A function that modifies the data (e.g., creating or deleting).
- **Options**: Callback functions for `onSuccess`, `onError`, etc.

---

## Prefetching Data

React Query allows you to prefetch data before it's needed using `queryClient.prefetchQuery`.

```jsx
queryClient.prefetchQuery('posts', fetchPosts);
```

---

## Query Invalidation

Invalidate queries to refresh the cached data. This is often used after mutations or when data needs to be updated.

```jsx
const queryClient = useQueryClient();
queryClient.invalidateQueries('posts'); // Refetch data
```

---

## Full Fetch Status Lifecycle

React Query provides a rich set of status flags to track the query's state:

1. **`isLoading`**: `true` when the query is fetching data for the first time.

   ```jsx
   if (isLoading) return <div>Loading...</div>;
   ```

2. **`isSuccess`**: `true` when the query has successfully fetched data.

   ```jsx
   if (isSuccess) {
     return (
       <ul>
         {data.map(post => (
           <li key={post.id}>{post.title}</li>
         ))}
       </ul>
     );
   }
   ```

3. **`isError`**: `true` if the query failed to fetch data.

   ```jsx
   if (isError) return <div>Error: {error.message}</div>;
   ```

4. **`isFetching`**: `true` when the query is fetching data, even during background updates.

   ```jsx
   {isFetching && <div>Refreshing...</div>}
   ```

5. **`isRefetching`**: `true` when a query is refetching (after initial fetch).

   ```jsx
   {isRefetching && <div>Refetching...</div>}
   ```

6. **`isIdle`**: `true` if the query is not actively fetching.

   ```jsx
   if (isIdle) return <div>Waiting to fetch data...</div>;
   ```

7. **`isSettled`**: `true` when the query has either succeeded or failed.

   ```jsx
   if (isSettled) {
     return error ? <div>Error: {error.message}</div> : <div>Data fetched!</div>;
   }
   ```

8. **`status`**: A single status field providing the current query state (`'loading'`, `'error'`, or `'success'`).

   ```jsx
   if (status === 'loading') return <div>Loading...</div>;
   if (status === 'error') return <div>Error occurred!</div>;
   if (status === 'success') return <div>Data loaded successfully!</div>;
   ```

---

## Advanced Features

### Caching and Stale Time

You can control how long data is considered "fresh" using the `staleTime` option.

```jsx
useQuery('posts', fetchPosts, { staleTime: 5000 }); // Data stays fresh for 5 seconds
```

### Polling / Background Refetching

Automatically refetch data at regular intervals using the `refetchInterval` option.

```jsx
useQuery('posts', fetchPosts, { refetchInterval: 10000 }); // Refetch every 10 seconds
```

### Manual Refetching

To trigger a manual refetch, use the `refetch` function returned by `useQuery`.

```jsx
const { refetch } = useQuery('posts', fetchPosts);

<button onClick={() => refetch()}>Refetch Posts</button>;
```

---

## Query Devtools (Optional)

For debugging and inspecting your queries, use the **React Query Devtools**.

```bash
npm install @tanstack/react-query-devtools
```

```jsx
import { ReactQueryDevtools } from '@tanstack/react-query-devtools';

function App() {
  return (
    <QueryClientProvider client={queryClient}>
      {/* Your app components */}
      <ReactQueryDevtools initialIsOpen={false} />
    </QueryClientProvider>
  );
}
```

---

## Summary of Common Hooks and Features:
- **`useQuery`**: Fetch and manage server-side data.
- **`useMutation`**: Modify server-side data (POST, PUT, DELETE).
- **`QueryClient`**: Manage caching and query state.
- **`useQueryClient`**: Access the `QueryClient` to invalidate or refetch queries.
- **`prefetchQuery`**: Preload data before it is needed.
- **Options**: Control caching, refetching, and data freshness (`staleTime`, `refetchInterval`, etc.).

---

This guide provides an overview of **React Query** and its powerful data-fetching capabilities. For more advanced use cases, refer to the [official documentation](https://tanstack.com/query/latest).