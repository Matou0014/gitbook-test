---
description: Keeping your Feedbacky instance up to date or migrating to a new host.
---

# Maintenance

{% hint style="info" %}
This section only concern system administrators who already have Feedbacky installed.
{% endhint %}

## Staying up to date

Keeping Feedbacky up to date is simple, keep and eye out for new versions on the [Docker Hub](https://hub.docker.com/u/plajer).

1\. Go to your Feedbacky directory.

```
cd /etc/feedbacky
```

2\. Type the following command, it will automatically pull the latest image available.

```
sudo docker compose pull
```

## Backup and Exporting

The following steps will help you move your Feedbacky instance to a new host or simple keep your Feedbacky data safe.

{% hint style="warning" %}
Cloud users (app.feedbacky.net) currently cannot backup their data.
{% endhint %}

1\. Go to your Feedbacky directory.

```
cd /etc/feedbacky
```

2\. Create a backup of your Feedbacky volume.

```
docker run --rm --volumes-from feedbacky-client -v $(pwd):/backup alpine tar cvfz /backup/feedbacky_backup.tar /storage-data
```

* `--rm` removes the container after exiting.
* `--volumes-from feedbacky-client` attach the volume used by the container.
* `-v $(pwd):/backup` writes the backup file into the current directory to the container.
* `alpine` is a small image used for the backup process.
* `tar cvfz /backup/feedbacky_backup.tar /storage-data` moves the volume's data into the backup file.

3\. Export your `.env` file and your newly created volume backup to the target host.

{% hint style="info" %}
You can find the exported files in your home directory, which you can then move back again to your Feedbacky directory on the target host.
{% endhint %}

```
scp .env feedbacky_backup.tar {USERNAME}@{ADDRESS}:
```

| `{USERNAME}` | The username of your account on the target host. |
| ------------ | ------------------------------------------------ |
| `{ADDRESS}`  | The IP Address or domain on the target host.     |

4\. On the target host, move the exported files in to your Feedbacky directory.

```
mv .env feedbacky_backup.tar /etc/feedbacky
```

5\. You can now migrate your data to Feedbacky on the target host.

{% hint style="info" %}
The migrate command is similar to one used for the backup with the addition of functions to upload the volume's data to Feedbacky on your target host.
{% endhint %}

```
docker run --rm --volumes-from feedbacky-client -v $(pwd):/backup alpine sh -c "cd /storage-data && tar xvf /backup/feedbacky_backup.tar --strip 1"
```
