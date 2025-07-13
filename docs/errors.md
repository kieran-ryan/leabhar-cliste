# Errors

A good error message should make it self-evident

- what the user did
- what the acceptable inputs are
- how to fix the problem

```
ConfigError: can't find 'ffprobe' to extract video metadata; have you run `brew install ffmpeg`
```

...rather than...

```
FileNotFoundError: [Errno 2] No such file or directory
```

## References

- _[Error-Message Guidelines](https://www.nngroup.com/articles/error-message-guidelines/)_, Tim Neusesser and Evan Sunwall
- [Exceptionally Tricky: Good errors in bad situations](https://youtu.be/2ziiIu_Xl2o?si=uH-Dkhk_8XSERjL2), Alistair Lynn
