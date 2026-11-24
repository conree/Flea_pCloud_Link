# pCloud Share Link for Flea

A [Flea](https://github.com/thisisgm/flea) plugin that adds **Copy pCloud Link** to the file menu.
Right-click a file or folder in your pCloud Drive (`~/pCloudDrive`), choose **Copy pCloud Link**,
and a public pCloud share link is put on your clipboard, ready to paste.

Select several items to copy one link per line.

## Requirements

- [rclone](https://rclone.org) with a pCloud remote named `pcloud`. Create it once (it opens
  pCloud's sign-in page in your browser):

  ```sh
  rclone config create pcloud pcloud
  ```

- `wl-copy` (from `wl-clipboard`) and `systemd-run` (part of systemd).
- Python 3.

## Install

```sh
flea plugin add https://github.com/conree/Flea_pCloud_Link.git
flea plugin enable si.pcloud-link
```

Then restart Flea so the menu item appears.

## Notes

- The links are **public**: anyone who has one can open or download the item, the same as a link
  made on pCloud's website. You can remove links from pCloud's shared-links list.
- Flea can't limit a plugin's menu item to one folder, so **Copy pCloud Link** shows on every file.
  Outside `~/pCloudDrive` it says that only pCloud Drive items have links.
- Flea runs plugins with a 512 MiB address-space limit, which is too little for rclone (a Go
  program) to start. The plugin therefore runs rclone as a short-lived unit of your user's
  systemd manager (`systemd-run --user --pipe --wait`).
- Nothing is sent anywhere except the share-link request rclone makes to pCloud.

## Licence

MIT. See [LICENSE](LICENSE).
