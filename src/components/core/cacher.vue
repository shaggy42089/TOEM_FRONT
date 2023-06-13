<script>
    const cacheKey = 'data';

    export function saveToCache(data) {
        console.log(data)
        localStorage.setItem(cacheKey, JSON.stringify(data))
    }

    export function getFromCache() {
        return JSON.parse(localStorage.getItem(cacheKey))
    }
</script>