Single header file watcher written in C++ suitable for watching creation, deletion, and modification of single files.

## Example

```cpp
// Watches for changes to the file at 'file.txt' once per second.
filewatch::FileWatcher watcher(
    "file.txt",
    std::chrono::milliseconds(1000)
);

// Sample callback.
const auto on_file_change = [](
    const std::string& path,
    const filewatch::EventKind event_kind)
{
    std::cout "change to " << path << ": ";

    switch (event_kind) {
        case filewatch::EventKind::Created:
            std::cout << "created" << std::endl; break;
        case filewatch::EventKind::Deleted:
            std::cout << "deleted" << std::endl; break;
        case filewatch::EventKind::Modified:
            std::cout << "modified" << std::endl; break;
        default: break;
    }
};

// Start the watcher on a separate thread.
std::thread watcher_thread([&watcher, &on_file_change]() {
    watcher.start(on_file_change);
});

// Stop the watcher.
watcher.stop();
watcher_thread.join();
```