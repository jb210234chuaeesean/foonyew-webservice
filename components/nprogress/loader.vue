<script setup>
useRouter().beforeEach(() => {
  NProgress.start()
})

useRouter().afterEach(() => {
  NProgress.done()
})
</script>

<script>
import NProgress from 'nprogress'
export default {
    beforeMount() {
        NProgress.start()
        setTimeout(() => {
            NProgress.done()
        }, 1000)
    },
}
</script>