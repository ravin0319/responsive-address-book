<template>
    <div class="contact-list">

        <div class="contact-list__title-and-dropdown">
            <h1 class="contact-list__title">My Contacts</h1>
            <select id="sortOrder" v-model="sortOrder" @change="sortContacts">
                <option value="ascending">ascending</option>
                <option value="descending">descending</option>
            </select>
        </div>

        <div v-if="loading" class="contact-list__loading">Loading...</div>
        <div v-else class="contact-list__grid">
            <ContactCard v-for="(contact, index) in sortedContacts" :key="index" :contact="contact" />
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import ContactCard from './ContactCard.vue';

export default {
    components: {
        ContactCard
    },
    data() {
        return {
            contacts: [],
            sortOrder: 'ascending', // Default to A-Z sorting
            loading: true
        };
    },
    computed: {
        sortedContacts() {
            return [...this.contacts].sort((a, b) => {
                const nameA = a.name.first.toLowerCase() + a.name.last.toLowerCase();
                const nameB = b.name.first.toLowerCase() + b.name.last.toLowerCase();

                if (this.sortOrder === 'ascending') {
                    return nameA.localeCompare(nameB);
                } else {
                    return nameB.localeCompare(nameA);
                }
            });
        }
    },
    created() {
        this.fetchContacts();
    },
    methods: {
        async fetchContacts() {
            try {
                const response = await axios.get('https://randomuser.me/api/?results=10');
                this.contacts = response.data.results;
            } catch (error) {
                console.error('Error fetching contacts:', error);
            } finally {
                this.loading = false;
            }
        },
        sortContacts() {
            // The sort is automatically triggered by changing `sortOrder` due to the computed property.
        }
    }
};
</script>

<style lang="scss" scoped>
.contact-list {
    width: 100%;
    margin: 0;

    &__title {
        font-weight: 400;
        font-size: 32px;
        color: #EF8100;
    }

    &__title-and-dropdown {
        display: flex;
        justify-content: space-between;
        align-items: center;

        select {
            padding: 8px;
            font-size: 1rem;
            border-radius: 5px;
            border: 1px solid #ddd;
            outline: none;
            cursor: pointer;
            border: 1px solid #000;
        }
    }

    &__grid {
        display: grid;
        grid-template-columns: 1fr;
        gap: 20px;
    }

    &__loading {
        text-align: center;
        font-size: 1.5rem;
        color: #777;
    }

    @media (min-width: 769px) {
        width: 729px;
        margin: 0 auto;
    }

    @media (min-width: 431px) and (max-width: 640px) {
        &__grid {
            grid-template-columns: 1fr 1fr;
        }
    }
}
</style>