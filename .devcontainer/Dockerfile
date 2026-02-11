# 使用 .NET 8 开发容器作为基础（已含 .NET SDK、Git 等）
FROM registry.qlaq2435.space/homelab/devcontainers-dotnet:8.0-bookworm-slim


# 设置版本（与你的文件名一致）
ENV GODOT_VERSION="4.6"

# 安装解压工具
RUN apt-get update && \
    apt-get install -y unzip && \
    rm -rf /var/lib/apt/lists/*

# 将本地文件复制到容器中
COPY Godot_v${GODOT_VERSION}-stable_mono_linux_x86_64.zip /tmp/
COPY Godot_v${GODOT_VERSION}-stable_mono_export_templates.tpz /tmp/

# 安装 Godot 引擎（无头版）
RUN unzip -q /tmp/Godot_v${GODOT_VERSION}-stable_mono_linux_x86_64.zip -d /usr/local/share/ && \
    mv /usr/local/share/Godot_v${GODOT_VERSION}-stable_mono_linux_x86_64/Godot_v${GODOT_VERSION}-stable_mono_linux.x86_64 /usr/local/bin/godot && \
    chmod +x /usr/local/bin/godot && \
    rm /tmp/Godot_v${GODOT_VERSION}-stable_mono_linux_x86_64.zip

# 安装导出模板（关键！路径必须精确匹配 godot --version 输出）
RUN mkdir -p ~/.local/share/godot/export_templates/${GODOT_VERSION}.stable.mono && \
    unzip -q /tmp/Godot_v${GODOT_VERSION}-stable_mono_export_templates.tpz -d ~/.local/share/godot/export_templates/${GODOT_VERSION}.stable.mono && \
    rm /tmp/Godot_v${GODOT_VERSION}-stable_mono_export_templates.tpz
# 验证安装
RUN godot --version