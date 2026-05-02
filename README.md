~~~
cat > /usr/bin/passwall << 'EOF'
#!/bin/sh

case "$1" in
    update)
        echo "Mengupdate config passwall..."
        
        wget --no-check-certificate -qO /tmp/passwall.tmp https://raw.githubusercontent.com/wifikunetworks/scripts/refs/heads/main/passwall
        
        if [ $? -eq 0 ] && [ -s /tmp/passwall.tmp ]; then
            cp /etc/config/passwall /etc/config/passwall.bak
            mv /tmp/passwall.tmp /etc/config/passwall
            echo "Config passwall berhasil diupdate!"
            /etc/init.d/passwall restart
            echo "Passwall direstart."
        else
            echo "GAGAL! Cek URL atau koneksi internet."
            rm -f /tmp/passwall.tmp
        fi
        ;;
    *)
        echo "Usage: passwall update"
        ;;
esac
EOF
chmod +x /usr/bin/passwall
~~~
