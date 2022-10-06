Find things with grep

```grep -R 'your string' dest```

Find all images and sort them by size

``find . -type f \( -iname \*.jpg -o -iname \*.png \) -exec du -ch {} + | sort -r -h``


