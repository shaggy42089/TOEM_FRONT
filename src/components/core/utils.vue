<script>
    import { hostStatuses } from './constants.vue'

    export function hostStatusToColor(status) {
        switch(status) {
            case hostStatuses.RUNNING:
                return "success"
            case hostStatuses.OFFLINE:
                return "danger"
            case hostStatuses.IDLE:
                return "warning"
            case hostStatuses.STOPPED:
                return "dark"
            default:
                return "danger"
        }
    }
</script>