# sqlite-path Documentation

A full reference to every function and module that sqlite-path offers.

As a reminder, sqlite-path follows semver and is pre v1, so breaking changes are to be expected.

## API Reference

<h3 name=path_version> <code>path_version()</code></h3>

Returns the semver version string of the current version of sqlite-path.

```sql
select path_version();
-- "v0.0.0"
```

<h3 name=path_debug> <code>path_debug()</code></h3>

Returns a debug string of various info about sqlite-path, including
the version string, build date, commit hash, and cwalk version.

```sql
select path_debug();
/*
Version: v0.0.0
Date: 2022-08-19T17:27:14Z-0700
Source: 01cd76716130b739f3e33177740e92e7ad0cff35
cwalk version: v1.2.6
*/
```

<h3 name=path_absolute> <code>path_absolute(path)</code></h3>

Returns 1 if the given path is absolute, 0 otherwise.

```sql
select path_absolute("/usr/local/bin"); -- 1
select path_absolute("./rel/to/me"); -- 0
```

<h3 name=path_basename> <code>path_basename(path)</code></h3>

Returns the basename of the given path as text,
or NULL if it cannot be calculated.

```sql
select path_basename('movies/spiderman.mp4');
-- "spiderman.mp4"
```

<h3 name=path_dirname> <code>path_dirname(path)</code></h3>

Returns the dirname of the given path as text, or NULL if it cannot be calculated.

```sql
select path_dirname('movies/spiderman.mp4');
-- "movies/"
```

<h3 name=path_extension> <code>path_extension(path)</code></h3>

Returns the extension of the given path as text, or NULL if it cannot be calculated.

```sql
select path_extension('spiderman.mp4'); -- ".mp4"
select path_extension('CHANGELOG'); -- NULL
```

<h3 name=path_intersection> <code>path_intersection(path)</code></h3>

Returns the common portions between two paths, or null if it cannot be computed.

```sql
SELECT path_intersection('/foo/bar/a', '/foo/bax/a');
-- "/foo"
```

<h3 name=path_join> <code>path_join(path1, path2, [...pathN])</code></h3>

Join two or more paths together, or null if it cannot be computed.

```sql
select path_join('src', 'index.js'); -- 'src/index.js'
select path_join('a', 'b', 'c'); -- 'a/b/c'
-- ""
```

<h3 name=path_normalize> <code>path_normalize(path)</code></h3>

Create a normalized version of the given path (resolving back segments), or null if it cannot be computed. path_relative(path) Returns 1 if the given path is relative, 0 if not, or null if path is null.

```sql
select path_normalize();
-- ""
```

<h3 name=path_root> <code>path_root(path)</code></h3>

Returns the root portion of the given path, or null if it cannot be computed.

```sql
select path_root();
-- ""
```

<h3 name=path_segment_at> <code>path_segment_at(path, at)</code></h3>

Returns the path segment in the given path at the specified index.
If 'at' is positive, then '0' is the first segment and counts to the end. If 'at' is negative, then '-1' is the last segment and continue to the beginning. If 'at' "overflows" in either direction, then returns NULL.

```sql
select path_segment_at();
-- ""
```

<h3 name=path_segments> <code>select * from path_segments(path)</code></h3>

Table function that returns each segment for the given path.
Return a table with the following schema:

```sql
create table path_segments(
 type text,        --
 segment text,     --x
 path text hidden  -- input path
)
```