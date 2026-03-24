# ============================================
# Evote Client - Web UI
# Blockchain Voting System
# ============================================

FROM nginx:alpine

# Copy static web files
COPY static/ /usr/share/nginx/html/

EXPOSE 3000

CMD ["nginx", "-g", "daemon off;"]
