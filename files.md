
cd /mnt/nas/daily_backup
git clone git@github.com:kxk254/blm-homepage
git clone git@github.com:kxk254/clientmanage
git clone git@github.com:kxk254/receipt
git clone git@github.com:kxk254/invoice
git clone git@github.com:kxk254/solitonre

create auto pull script

nano ~/git_autopull.sh

#!/bin/bash
BASE_DIR="/mnt/nas/daily_backup"

repos=(
    "blm-homepage" 
    "clientmanage" 
    "receipt"
    "invoice"
    "solitonre"
)

for repo in "${repos[@]}"; do
echo "==== Updating $repo ===="
cd "$BASE_DIR/$repo" || {
    echo "Failed to enter $repo"
    continue
}
git pull --rebase
done

# make executable:
chmod +x ~/git_autopull.sh

# Schedule daily cron

crontab -e 

Add:
30 2 * * * /home/konno/git_autopull.sh >> /mnt/konno/git_autopull.log 2>&1

