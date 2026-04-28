~~~
cat > /usr/bin/passwall << 'EOF'
#!/bin/sh

case "$1" in
    update)
        echo "Mengupdate config passwall..."
        wget -qO /etc/config/passwall https://github.com/wifikunetworks/scripts/raw/refs/heads/main/passwall
        if [ $? -eq 0 ]; then
            echo "Config passwall berhasil diupdate!"
            /etc/init.d/passwall restart
            echo "Passwall direstart."
        else
            echo "GAGAL! Cek URL atau koneksi internet."
        fi
        ;;
    *)
        echo "Usage: passwall update"
        ;;
esac
EOF
chmod +x /usr/bin/passwall
~~~
