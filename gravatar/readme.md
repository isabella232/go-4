## go-gravatar

Simple go library to interact with Gravatar.

## Usage

If you already have the hash, build a new Gravatar object and generate its url like so:

    g := NewGravatar()
    g.Hash = "hash-goes-here"
    url := g.GetURL()

If you have an email address:

    g := NewGravatarFromEmail("foo@example.com")
    url := g.GetURL()

If you have a WordPress.com username:

    g := NewGravatarFromUsername("mkaz")
    url := g.GetURL()


## Gravatar Profile

Gravatar profile information is available, if entered in by the user

```
    Hash        - Gravatar Hash
    ProfileUrl  - Link to Gravatar Profile
    DisplayName - Display name for user
    AboutMe     - Short bio
    Accounts    - External accounts, includes domain, username, url
```

To fetch Gravatar Profile using WordPress.com username

    gp := FetchGravatarProfileByUsername("mkaz")



## Contributors

You? Pull requests welcome.


## License

[GNU General Public License, version 2](http://www.gnu.org/licenses/gpl-2.0.html)
